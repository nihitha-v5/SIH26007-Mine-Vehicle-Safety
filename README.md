# SIH26007 – Safe and Efficient Operation of Mine Vehicles in Fog and Low-Visibility Conditions

## About the Project

Working in open-cast iron ore mines becomes more difficult when fog, dust, darkness or other low-visibility conditions reduce the driver's view.

In these situations, it can become difficult for mine vehicle operators to identify nearby vehicles, obstacles and changes in the road in enough time.

Our project proposes a smart safety system that combines information from multiple sensors and vehicle data to understand the surroundings, estimate collision risk and give the driver an appropriate warning.

The main idea is simple:

**Sense → Understand → Predict → Assess → Warn → Learn**

---

## Problem

Mine vehicles such as haul trucks operate in large mining areas where visibility can change quickly.

During fog and low-visibility conditions, the operator may not get enough visual information about:

* Nearby vehicles
* Obstacles
* Vehicle movement
* Road conditions
* Turns and restricted areas
* Possible collision situations

A system that can combine information from different sources and warn the operator before a dangerous situation develops can improve situational awareness and support safer vehicle operation.

---

## Our Proposed Solution

We are developing a multi-sensor safety system for mine vehicles.

The system collects information from sensors, vehicle-position data, communication between vehicles and the digital mine map.

This information is combined to create a common picture of the vehicle's surroundings.

The system then:

1. Detects nearby objects and vehicles.
2. Understands their movement.
3. Predicts possible future movement.
4. Calculates collision risk.
5. Gives a risk-based warning to the driver.
6. Stores important events for future safety analysis.

---

## System Approach

Our system follows six main stages:

```text
SENSE
  ↓
FUSE
  ↓
PREDICT
  ↓
ASSESS
  ↓
ADVISE
  ↓
LEARN
```

### SENSE

Collect information from radar, cameras, vehicle sensors, V2V communication and the mine map.

### FUSE

Combine the available information to create a common view of the vehicle's surroundings.

### PREDICT

Estimate the future movement of the vehicle and nearby objects and calculate Time to Collision (TTC).

### ASSESS

Determine the level of collision risk using factors such as distance, relative speed, TTC, visibility and road conditions.

### ADVISE

Give the driver a warning based on the calculated risk instead of treating every detected object in the same way.

### LEARN

Store important events such as near misses and repeated warnings to identify high-risk locations and improve future warnings.

---

## Main Inputs

The proposed system can use the following inputs:

| Input               | Purpose                                                     |
| ------------------- | ----------------------------------------------------------- |
| 77 GHz mmWave Radar | Distance, relative movement and obstacle detection          |
| IR/NIR Camera       | Detect vehicles, people and obstacles in reduced visibility |
| LWIR Thermal Camera | Additional sensing in darkness/fog                          |
| GNSS                | Vehicle position                                            |
| IMU                 | Vehicle movement and heading                                |
| Wheel Odometry      | Vehicle speed and distance travelled                        |
| V2V Communication   | Nearby vehicle information                                  |
| Digital Mine Map    | Road geometry, turns and restricted areas                   |

The exact sensors and modules used in the physical prototype are documented separately in the Hardware section.

---

## Collision Risk

One of the important values used by the system is **Time to Collision (TTC)**.

For a simple closing-speed situation:

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

This means that, if the current relative motion continues under the same assumptions, the estimated time before collision is approximately 3 seconds.

The system can use TTC along with visibility, vehicle type, road geometry, traffic and other information when assessing risk.

---

## Near-Miss Detection

Not every dangerous situation results in an actual collision.

For example:

A truck is travelling at 20 km/h and another vehicle suddenly crosses its path. The estimated TTC falls to 1.8 seconds, but the truck slows down and the collision is avoided.

We treat this type of event as a near miss.

Instead of ignoring the event, the system can store the location and conditions associated with it.

If similar near misses happen repeatedly at the same location, that area can be marked as a high-risk zone.

```text
Near-Miss Data
      ↓
Risk Analysis
      ↓
High-Risk Locations
      ↓
Risk Heatmap
      ↓
Preventive Action
```

---

## Warning System

The system is designed to provide risk-prioritized warnings.

For example:

```text
HIGH RISK

Vehicle approaching from left
Distance: 28 m
TTC: 4.2 seconds

Action: Reduce speed
```

Possible warning methods include:

* Audio warning
* Dashboard display
* HUD
* Recommended speed
* Direction of hazard
* Hazard location

---

## Hardware

The hardware part of the project consists of the sensing, processing, communication and warning components required for the prototype.

The complete component list and connections are available here:

# Hardware Components

The FOG-RISE prototype integrates sensing, positioning, communication, processing and driver-warning components to support safe HEMM operation during fog and low-visibility conditions.

| Component | Purpose |
|---|---|
| **77 GHz mmWave Radar** | Detects nearby objects, distance and relative motion, including in low-visibility conditions. |
| **IR/NIR Camera** | Helps detect vehicles, people and obstacles in fog and darkness. |
| **LWIR Thermal Camera (Optional)** | Provides thermal information for improved detection in poor visibility and low-light conditions. |
| **GNSS Module** | Provides vehicle position and supports location-based risk identification. |
| **IMU** | Measures vehicle motion, acceleration and heading changes. |
| **Wheel Odometry** | Provides vehicle speed and distance travelled. |
| **V2V Communication Module** | Exchanges vehicle position, speed and heading information with nearby vehicles. |
| **Processing Unit** | Receives and processes sensor and communication data for sensor fusion, trajectory prediction and risk assessment. |
| **Driver Display / HUD** | Displays risk information, warnings and recommended speed to the driver. |
| **Audio Warning Unit** | Provides immediate audible alerts when a high-risk situation is detected. |
| **Power Supply Unit** | Provides regulated power to the prototype's electronic components. |

# Hardware Connections

## Sensor Connections

- Radar → Processing Unit
- IR/NIR Camera → Processing Unit
- GNSS → Processing Unit
- IMU → Processing Unit
- Wheel Odometry → Processing Unit
- V2V Module → Processing Unit

## Warning System

- Processing Unit → Display
- Processing Unit → Buzzer/Audio Alert

## Power

- Power Supply → Processing Unit
- Power Supply → Sensors
- Power Supply → Communication and Warning Modules

Prototype photographs and the circuit diagram are also included in the Hardware folder.

---

## Software

The software part is responsible for processing the incoming data, combining information from different sources, estimating risk and generating warnings.

The source code and software details are available in:

`software/source-code`

---

## Testing

We are testing the system under different conditions to check:

* Detection of nearby objects
* Response to changing distance
* Collision-risk calculation
* Warning generation
* Behaviour under reduced visibility
* Response time
* Reliability of the prototype

Testing results will be documented in:

`testing/test-results.md`

---

## Expected Outcome

The aim of this project is to provide mine vehicle operators with better information about their surroundings during fog and low-visibility conditions.

The system is intended to support:

* Better situational awareness
* Earlier detection of possible hazards
* Risk-based warnings
* Safer vehicle movement
* Identification of repeated high-risk locations
* Improved safety planning in mine operations

---

## Future Scope

The system can be extended by:

* Improving sensor fusion
* Adding more vehicle-to-vehicle communication capabilities
* Improving performance in different visibility conditions
* Improving trajectory prediction
* Adding more detailed mine-map information
* Improving the risk model using collected events
* Conducting larger-scale field testing

---

## Project Status

**Current Stage:** Prototype Development and Testing

The hardware, software and system design are being integrated and tested as part of the SIH project.

---

## Team

This project is developed by our SIH team for:

**Smart India Hackathon – SIH26007**

Team member details are available here:

Team Members : 
- V NIHITHA
- CH. VIJAYA SPOORTHI
- GNANA PRASOONA .G
- DARSHINI DATLA
- AMULYA .A
- AKSHITHA .D

---

## Repository Structure

docs/       → Project documentation and technical approach
hardware/   → Components, connections and prototype
software/   → Software and source code
testing/    → Testing and observations
team/       → Team information
