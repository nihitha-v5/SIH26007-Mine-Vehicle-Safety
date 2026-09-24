# Software System

## 1. Overview

The software is the main decision-making part of the SIH26007 mine-vehicle safety system.

The purpose of the software is to collect information from different sensors and vehicle systems, combine the available information, understand the current situation around the vehicle, estimate the possibility of a collision, and provide an appropriate warning to the vehicle operator.

The system is designed especially for **fog and low-visibility conditions in open-cast iron ore mines**, where depending only on the driver's direct vision may not be sufficient.

The software follows the overall process:

```text
SENSE
  ↓
FUSE
  ↓
DETECT
  ↓
TRACK
  ↓
PREDICT
  ↓
ASSESS
  ↓
ADVISE
  ↓
STORE
  ↓
LEARN
```

---

# 2. Main Software Functions

The software is divided into several functional modules:

1. Sensor Data Collection
2. Data Synchronization
3. Sensor Fusion
4. Object Detection
5. Object Tracking
6. Vehicle State Monitoring
7. Trajectory Prediction
8. Time-to-Collision Calculation
9. Collision Risk Assessment
10. Warning Generation
11. Event Logging
12. Risk Heatmap Generation
13. Dashboard / Monitoring
14. Data Storage
15. System Monitoring

Each module has a specific role in converting raw sensor information into useful safety information.

---

# 3. Software Architecture

The overall software architecture is:

```text
                  SENSOR INPUTS
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
      Radar          Camera       Vehicle Data
                                      │
                              GNSS / IMU /
                              Wheel Data
        │              │              │
        └──────────────┼──────────────┘
                       │
                       ▼
              DATA COLLECTION
                       │
                       ▼
              DATA SYNCHRONIZATION
                       │
                       ▼
                SENSOR FUSION
                       │
              ┌────────┴────────┐
              │                 │
              ▼                 ▼
       OBJECT DETECTION    VEHICLE STATE
              │                 │
              └────────┬────────┘
                       ▼
                OBJECT TRACKING
                       │
                       ▼
              TRAJECTORY PREDICTION
                       │
                       ▼
              TTC CALCULATION
                       │
                       ▼
              RISK ASSESSMENT
                       │
              ┌────────┴─────────┐
              │                  │
              ▼                  ▼
       WARNING SYSTEM       EVENT STORAGE
              │                  │
              ▼                  ▼
          OPERATOR          RISK ANALYSIS
                                 │
                                 ▼
                            RISK HEATMAP
```

---

# 4. Sensor Data Collection

The first software stage receives information from the available hardware sensors.

Possible input sources include:

* 77 GHz mmWave radar
* IR/NIR camera
* LWIR thermal camera
* GNSS
* IMU
* Wheel odometry
* V2V communication
* Mine map information

Each source provides different types of information.

### Radar

Radar can provide information such as:

* Distance to an object
* Relative movement
* Relative speed
* Object position
* Presence of nearby objects

Radar information can be especially useful when visibility is poor.

### Camera

The camera can be used for visual object detection.

Possible objects include:

* Heavy mine vehicles
* Light vehicles
* People
* Obstacles
* Road-related objects

### GNSS

GNSS provides information about the vehicle's location.

This information can be used for:

* Vehicle position
* Location-based event recording
* High-risk area identification
* Route information

### IMU

The IMU provides information related to vehicle movement and orientation.

It can help determine:

* Acceleration
* Vehicle movement
* Orientation
* Change in direction

### Wheel Odometry

Wheel odometry can provide information related to:

* Vehicle speed
* Distance travelled
* Vehicle movement

### V2V Communication

Vehicle-to-vehicle communication can allow nearby vehicles to share information such as:

* Position
* Speed
* Heading
* Vehicle status

---

# 5. Data Synchronization

Different sensors may generate data at different times and frequencies.

Before combining the information, the software synchronizes the available data.

```text
Radar Data
     │
Camera Data
     │
GNSS Data
     │
IMU Data
     │
Vehicle Data
     │
     ▼
Data Synchronization
     │
     ▼
Common Time Reference
```

This helps the system compare information from different sensors correctly.

For example, the radar and camera should refer to approximately the same point in time when the system decides whether an object is approaching the vehicle.

---

# 6. Sensor Fusion

Sensor fusion combines information from different sources into a common representation of the surrounding environment.

```text
Radar ────────┐
Camera ───────┤
GNSS ─────────┤
IMU ──────────┤
Wheel Data ───┤
V2V ──────────┤
Mine Map ─────┘
       │
       ▼
 SENSOR FUSION
       │
       ▼
COMMON SITUATION PICTURE
```

Instead of depending on only one sensor, the system uses available information from multiple sources.

For example:

```text
Camera → identifies an object
Radar  → provides distance and relative movement
GNSS   → provides location
V2V    → provides information from another vehicle
```

The combined information can provide a better understanding of the current situation.

---

# 7. Object Detection

The object-detection module identifies objects around the vehicle.

Possible detected objects include:

* Dump trucks
* Haul trucks
* Light vehicles
* People
* Obstacles
* Other relevant objects

The detection output can contain:

```text
Object ID
Object Type
Position
Distance
Estimated Speed
Direction
Confidence
Timestamp
```

Example:

```text
Object ID: 12
Type: Mine Truck
Distance: 35 m
Relative Speed: 8 m/s
Direction: Same Lane
```

The exact detection capabilities depend on the sensors and machine-learning model used in the final implementation.

---

# 8. Object Tracking

Detection provides information about objects at a particular time.

Tracking maintains information about the same object over multiple time steps.

```text
Frame 1 → Object detected
Frame 2 → Same object detected
Frame 3 → Same object detected
Frame 4 → Object moving closer
```

Tracking helps estimate:

* Movement direction
* Speed change
* Distance change
* Object trajectory
* Whether the object is approaching or moving away

This information is important for calculating collision risk.

---

# 9. Vehicle State Monitoring

The system also monitors the state of the vehicle on which it is installed.

Important information can include:

* Current speed
* Position
* Heading
* Acceleration
* Direction of movement
* Road location
* Visibility condition

Example:

```text
Vehicle Speed: 22 km/h
Heading: North-East
Position: Mine Road Section A
Visibility: Low
```

This information is used together with detected-object information during risk assessment.

---

# 10. Trajectory Prediction

The system can estimate the future movement of the vehicle and nearby objects.

The prediction can consider:

* Current position
* Current speed
* Direction
* Heading
* Relative movement
* Road geometry
* Vehicle type
* Visibility
* Previous movement

A simplified representation is:

```text
Current Position
       ↓
Current Speed
       ↓
Direction / Heading
       ↓
Road Geometry
       ↓
Predicted Movement
```

The purpose is not only to detect where an object is now, but also to estimate whether its future path could create a dangerous situation.

---

# 11. Time-to-Collision (TTC)

Time-to-Collision is used to estimate how much time is available before two approaching objects could reach the same position if their current closing movement continues.

A simplified calculation is:

```text
TTC = Distance / Closing Speed
```

For example:

```text
Distance = 30 m
Closing Speed = 10 m/s

TTC = 30 / 10
    = 3 seconds
```

A smaller TTC generally means that less time is available to respond.

The actual risk decision should not depend only on TTC. Other factors such as vehicle type, visibility, road geometry and relative movement should also be considered.

---

# 12. Collision Risk Assessment

The risk-assessment module combines multiple factors to estimate the current level of collision risk.

Possible factors include:

* Distance
* Relative speed
* TTC
* Vehicle speed
* Vehicle type
* Direction of movement
* Visibility
* Road geometry
* Traffic density
* Relative position
* Predicted trajectory

A conceptual flow is:

```text
Distance
   +
Relative Speed
   +
TTC
   +
Visibility
   +
Road Geometry
   +
Vehicle Information
   +
Trajectory
   │
   ▼
RISK ASSESSMENT
   │
   ▼
Risk Level
```

The system can represent the risk using categories such as:

```text
LOW
MEDIUM
HIGH
CRITICAL
```

These categories should be configured and validated during testing.

---

# 13. Dynamic Risk Updating

Risk is not treated as a fixed value.

As the vehicle moves, the system continuously receives new information.

For example:

```text
Initial Situation
Distance = 60 m
TTC = 15 sec
Risk = Low

        ↓

Vehicle approaches

Distance = 40 m
TTC = 8 sec
Risk = Medium

        ↓

Vehicle continues approaching

Distance = 20 m
TTC = 3 sec
Risk = High
```

This allows the warning level to change according to the current situation.

---

# 14. Visibility-Aware Risk Assessment

Fog and low visibility are major parts of the SIH problem.

The software can include visibility as an additional factor in the risk assessment.

For example:

```text
Normal Visibility
      ↓
Normal Detection Range

Reduced Visibility
      ↓
Reduced Effective Visibility Range
      ↓
Higher Attention Required

Very Low Visibility
      ↓
Earlier / Stronger Warning
```

The exact thresholds should be determined through testing and field validation.

---

# 15. Near-Miss Detection

The system can also identify situations where a collision risk becomes high but an actual collision does not occur.

Example:

```text
Vehicle A approaches Vehicle B
          ↓
TTC becomes very low
          ↓
High-risk situation detected
          ↓
Vehicle slows down
          ↓
No collision
          ↓
Near-miss recorded
```

The event can be stored with information such as:

* Time
* Location
* Vehicle information
* Distance
* TTC
* Speed
* Visibility
* Risk level
* Event type

Repeated near-miss events at the same location can indicate a possible high-risk area.

---

# 16. Warning Generation

The warning module converts the calculated risk into information that the vehicle operator can understand quickly.

The warning can include:

* Risk level
* Object direction
* Distance
* TTC
* Recommended attention/action
* Audio warning
* Visual warning

Example:

```text
⚠ HIGH RISK

Vehicle approaching from left

Distance: 28 m
TTC: 4.2 seconds

Action: Reduce speed
```

The warning should be simple and easy to understand because the operator may have very little time to react.

---

# 17. Risk-Prioritized Alerts

The system should not provide the same warning for every detected object.

Instead, warnings can be prioritized according to the estimated risk.

```text
LOW RISK
     ↓
Information / No urgent alert

MEDIUM RISK
     ↓
Attention warning

HIGH RISK
     ↓
Strong warning

CRITICAL RISK
     ↓
Immediate safety alert
```

This can help reduce unnecessary warnings and allow the operator to focus on important situations.

---

# 18. Warning Information

A warning may contain:

```text
Risk Level
     +
Object Type
     +
Direction
     +
Distance
     +
TTC
     +
Vehicle Speed
```

Example:

```text
HIGH RISK

Object: Heavy Vehicle
Direction: Front-Right
Distance: 24 m
TTC: 3.5 sec

Reduce Speed
```

The final warning format depends on the output hardware used in the prototype.

---

# 19. Event Logging

Important safety events can be stored for later analysis.

The system can record:

* Collision-risk events
* Near-miss events
* Repeated warnings
* High-risk locations
* Visibility conditions
* Vehicle speed
* Object information
* TTC
* Date and time

Example event:

```text
Event Type: Near Miss
Location: Mine Road Section B
Vehicle Speed: 21 km/h
TTC: 2.4 sec
Visibility: Low
Risk Level: High
Time: 10:32 AM
```

---

# 20. Risk Heatmap

The stored safety events can be analyzed to identify locations where risky situations occur repeatedly.

```text
Safety Events
      ↓
Location Analysis
      ↓
Repeated Risk Areas
      ↓
Risk Classification
      ↓
Risk Heatmap
```

The heatmap can help mine management identify areas where additional safety measures may be required.

Possible high-risk areas may include:

* Sharp turns
* Intersections
* Narrow roads
* Frequently used haul-road sections
* Areas with repeated low-visibility incidents

The actual high-risk locations should be determined from collected data rather than assumed in advance.

---

# 21. Mine Map Integration

The software can use digital mine-map information along with sensor data.

Possible map information includes:

* Road layout
* Road direction
* Turns
* Intersections
* Restricted areas
* High-risk locations
* Vehicle routes

Example:

```text
Sensor Data
     +
Vehicle Location
     +
Mine Map
     │
     ▼
Road-Aware Risk Assessment
```

This can help the system understand the surrounding road environment.

---

# 22. V2V Data Processing

When vehicle-to-vehicle communication is available, information from nearby vehicles can be included in the software.

Example:

```text
Vehicle A
Position: X1
Speed: 20 km/h
Heading: North

        │
        │ V2V
        ▼

Vehicle B
Position: X2
Speed: 18 km/h
Heading: South
```

The software can combine this information with local sensor observations to improve situational awareness.

---

# 23. Dashboard / Monitoring Interface

A software dashboard can be used to monitor the system.

The dashboard may display:

* Current vehicle status
* Vehicle speed
* Nearby objects
* Object distance
* TTC
* Current risk level
* Visibility status
* Active warnings
* Recent safety events
* High-risk locations
* Risk heatmap

Example layout:

```text
┌─────────────────────────────────────────┐
│        MINE VEHICLE SAFETY SYSTEM       │
├─────────────────────────────────────────┤
│ Vehicle Speed: 22 km/h                  │
│ Visibility: LOW                          │
│ Risk Level: HIGH                         │
├─────────────────────────────────────────┤
│ Nearby Objects                           │
│                                         │
│ Truck     28 m     TTC: 4.2 sec         │
│ Vehicle   45 m     TTC: 9.5 sec         │
├─────────────────────────────────────────┤
│             ACTIVE WARNING              │
│        VEHICLE APPROACHING              │
│             REDUCE SPEED                │
└─────────────────────────────────────────┘
```

---

# 24. Data Storage

The software can maintain a database or structured storage system for safety events.

Possible stored information:

| Field          | Description                       |
| -------------- | --------------------------------- |
| Event ID       | Unique event number               |
| Date/Time      | Time of event                     |
| Location       | Vehicle location                  |
| Vehicle Speed  | Speed during event                |
| Object Type    | Detected object                   |
| Distance       | Distance from object              |
| Relative Speed | Relative movement                 |
| TTC            | Estimated time to collision       |
| Visibility     | Visibility condition              |
| Risk Level     | Calculated risk                   |
| Event Type     | Warning / near-miss / other event |

This data can later be used for analysis and improvement.

---

# 25. Software Data Flow

The complete software data flow is:

```text
Sensor Data
     ↓
Data Collection
     ↓
Data Cleaning
     ↓
Data Synchronization
     ↓
Sensor Fusion
     ↓
Object Detection
     ↓
Object Tracking
     ↓
Vehicle State Monitoring
     ↓
Trajectory Prediction
     ↓
TTC Calculation
     ↓
Risk Assessment
     ↓
Warning Generation
     ↓
Operator Alert
     ↓
Event Logging
     ↓
Risk Analysis
     ↓
Risk Heatmap
```

---

# 26. Data Validation

Before using sensor information for risk assessment, the software should check whether the data is valid.

Possible checks include:

* Missing sensor data
* Invalid values
* Sudden unrealistic changes
* Communication failure
* Sensor failure
* Timestamp mismatch

If a sensor becomes unavailable, the system should identify the problem rather than silently treating missing information as valid data.

---

# 27. Fault Handling

The system should be designed to handle sensor or communication problems.

Example:

```text
Sensor Working
      ↓
Normal Processing

Sensor Failure
      ↓
Failure Detected
      ↓
System Status Updated
      ↓
Operator / System Warning
```

Possible faults include:

* Radar unavailable
* Camera unavailable
* GNSS signal loss
* Communication failure
* Processing failure
* Invalid sensor values

The exact fault-response behaviour should be defined according to the final prototype.

---

# 28. Software Technology

The final technology list should contain only the technologies actually used by the team.

Possible categories are:

| Category             | Technology Used            |
| -------------------- | -------------------------- |
| Programming Language | Add actual language        |
| Computer Vision      | Add actual library/model   |
| Machine Learning     | Add actual framework/model |
| Backend              | Add actual framework       |
| Frontend             | Add actual framework       |
| Database             | Add actual database        |
| Communication        | Add actual protocol/module |
| Hardware Interface   | Add actual interface       |

### Example

```text
Programming Language : Python
Backend              : FastAPI
Frontend              : Add actual frontend technology
Computer Vision       : Add actual CV library/model
Database              : Add actual database
Hardware Interface    : Add actual interface
```

**Do not list a technology just because it is planned.**

---

# 29. Machine Learning / AI

If machine-learning models are used in the implementation, they can support tasks such as:

* Vehicle detection
* Object detection
* Object classification
* Object tracking
* Image-based visibility analysis
* Anomaly detection

A general AI workflow is:

```text
Training Dataset
      ↓
Data Preparation
      ↓
Model Training
      ↓
Model Validation
      ↓
Model Testing
      ↓
Trained Model
      ↓
Real-Time Input
      ↓
Prediction
```

The model should be trained and tested using suitable datasets representing the intended operating conditions.

If a model is still under development, it should be marked as **Under Development** rather than presented as fully implemented.

---

# 30. Model Training Data

Training data may contain images or sensor information representing different situations.

Possible categories include:

* Mine vehicles
* Heavy trucks
* Light vehicles
* People
* Obstacles
* Fog conditions
* Reduced visibility
* Normal visibility

The dataset should be properly organized and labelled before model training.

Example:

```text
dataset/
│
├── train/
│   ├── images/
│   └── labels/
│
├── validation/
│   ├── images/
│   └── labels/
│
└── test/
    ├── images/
    └── labels/
```

Only datasets that are legally available for the intended use should be included.

Large datasets do not necessarily need to be uploaded directly into the GitHub repository. Dataset links, instructions and metadata can be documented instead.

---

# 31. Real-Time Processing

For a practical safety system, the software should process incoming information continuously.

```text
Sensor Input
     ↓
Process Current Data
     ↓
Update Object Information
     ↓
Calculate TTC
     ↓
Update Risk
     ↓
Generate Warning
     ↓
Store Event if Required
     ↓
Receive New Data
     ↺
```

This continuous cycle allows the system to respond to changing vehicle and environmental conditions.

---

# 32. Software Response Example

Consider a vehicle travelling through a foggy mine road.

```text
Step 1:
Vehicle is moving at 22 km/h.

Step 2:
Radar detects another vehicle ahead.

Step 3:
Camera provides supporting object information.

Step 4:
The system calculates distance and relative movement.

Step 5:
The system estimates TTC.

Step 6:
Visibility is identified as low.

Step 7:
Risk assessment combines TTC, distance,
speed, visibility and road information.

Step 8:
Risk increases to HIGH.

Step 9:
The operator receives a warning.

Step 10:
The event is stored for later analysis.
```

---

# 33. Example of Near-Miss Processing

```text
Nearby Vehicle Detected
          ↓
Distance Decreases
          ↓
TTC Becomes Small
          ↓
High Risk Detected
          ↓
Warning Generated
          ↓
Driver Slows Down
          ↓
Collision Avoided
          ↓
Near-Miss Event Stored
          ↓
Location Added to Risk Analysis
```

This allows the system to learn from situations where a collision was avoided.

---

# 34. Software Security

The software should protect system data and prevent unauthorized changes.

Basic measures can include:

* Secure configuration
* Access control
* Protection of sensitive credentials
* No API keys in the GitHub repository
* Input validation
* Safe database access
* Proper error handling

Sensitive files such as:

```text
.env
API keys
Passwords
Private credentials
```

should not be uploaded to GitHub.

---

# 35. Performance Considerations

The software should aim to provide safety information with low delay.

Important considerations include:

* Sensor processing time
* Model inference time
* Data synchronization delay
* Communication delay
* TTC calculation time
* Warning-generation delay
* Storage time

Testing should measure these values when the actual prototype is available.

---

# 36. Software Testing

The software should be tested under different operating conditions.

| Test    | Condition           | Expected Behaviour                                   |
| ------- | ------------------- | ---------------------------------------------------- |
| Test 1  | Normal visibility   | Objects detected and tracked                         |
| Test 2  | Reduced visibility  | System continues using available sensing information |
| Test 3  | Safe distance       | No unnecessary high-risk warning                     |
| Test 4  | Approaching vehicle | Distance and relative movement updated               |
| Test 5  | Low TTC             | Risk level increases                                 |
| Test 6  | High-risk situation | Warning generated                                    |
| Test 7  | Near miss           | Event recorded                                       |
| Test 8  | Sensor failure      | Fault identified                                     |
| Test 9  | Communication loss  | Communication status updated                         |
| Test 10 | Repeated events     | Location considered for risk analysis                |

Actual results should be added after testing.

---

# 37. Current Implementation Status

The software should clearly separate implemented and planned features.

### Currently Implemented

Add only the modules that are actually working in the current prototype.

```text
- Add implemented feature
- Add implemented feature
- Add implemented feature
```

### Under Development

```text
- Add feature currently being developed
- Add feature currently being tested
```

### Proposed / Future

```text
- Advanced trajectory prediction
- Expanded V2V integration
- Mine-wide risk heatmap
- Advanced AI models
- Additional sensor integration
```

The project documentation will be updated as development progresses.

---

# 38. Software Workflow Summary

The complete software workflow can be summarized as:

```text
SENSE
Collect sensor and vehicle information
        ↓
FUSE
Combine information from multiple sources
        ↓
DETECT
Identify nearby vehicles and obstacles
        ↓
TRACK
Monitor their movement
        ↓
PREDICT
Estimate future movement and TTC
        ↓
ASSESS
Calculate current collision risk
        ↓
ADVISE
Generate a suitable warning
        ↓
STORE
Record important safety events
        ↓
LEARN
Identify repeated high-risk situations
```

---

# 39. Expected Software Output

The software is expected to provide:

* Better awareness of nearby vehicles and obstacles
* Distance and movement information
* Time-to-Collision estimation
* Dynamic collision-risk assessment
* Risk-prioritized warnings
* Near-miss recording
* High-risk location identification
* Safety-event history
* Data for future safety analysis

---

# 40. Future Software Improvements

Future development can include:

* More advanced multi-sensor fusion
* Improved object detection in fog
* Better trajectory prediction
* More detailed mine-map integration
* Improved V2V communication
* Advanced risk prediction
* Mine-wide safety dashboard
* Historical safety analytics
* Automatic risk-heatmap updates
* Improved warning personalization
* Large-scale field testing
* Integration with mine fleet-management systems

---

# 41. Final Software Goal

The main goal of the software is to convert raw sensor and vehicle information into simple, useful and timely safety information.

```text
RAW DATA
   ↓
INFORMATION
   ↓
SITUATIONAL AWARENESS
   ↓
RISK ESTIMATION
   ↓
WARNING
   ↓
SAFER DECISION
```

The software is therefore not limited to object detection. It is intended to act as a **decision-support layer** that helps the vehicle operator understand potentially dangerous situations earlier, especially during fog and low-visibility conditions.
