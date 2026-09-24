# Hardware Components

## 1. Hardware Overview

The hardware part of the SIH26007 solution is designed to collect information about the mine vehicle, nearby vehicles, obstacles and surrounding conditions.

The collected information is sent to the processing unit, where the software performs object detection, sensor fusion, Time-to-Collision (TTC) calculation and collision-risk assessment.

The main hardware structure is:

```text
Sensors
   ↓
Processing Unit
   ↓
Data Processing
   ↓
Risk Assessment
   ↓
Warning / Display
```

---

# 2. Main Hardware Components

| S.No. | Component                    | Purpose                                                   |
| ----- | ---------------------------- | --------------------------------------------------------- |
| 1     | Raspberry Pi 5               | Main processing and control unit                          |
| 2     | USB / CSI Camera             | Captures the road and nearby objects                      |
| 3     | IR/NIR Camera Module         | Helps capture information in low-light conditions         |
| 4     | Ultrasonic Sensor            | Measures distance to nearby objects for prototype testing |
| 5     | GPS Module                   | Provides vehicle location                                 |
| 6     | MPU6050 IMU                  | Measures acceleration and orientation                     |
| 7     | Wheel Encoder                | Measures wheel rotation and helps estimate vehicle speed  |
| 8     | Buzzer                       | Provides an audio warning                                 |
| 9     | LED Indicators               | Provides visual risk indication                           |
| 10    | OLED/LCD Display             | Displays warning and vehicle information                  |
| 11    | Microcontroller              | Handles low-level sensor interfacing                      |
| 12    | Power Supply / Battery       | Provides power to the hardware                            |
| 13    | Jumper Wires & Connectors    | Used for hardware connections                             |
| 14    | Breadboard / Prototype Board | Used for prototype circuit assembly                       |
| 15    | Vehicle Prototype Chassis    | Represents the mine vehicle for testing                   |

---

# 3. Raspberry Pi 5

### Purpose

The Raspberry Pi acts as the main processing unit of the prototype.

It can receive data from the camera, sensors and microcontroller and pass the information to the software system.

### Main Responsibilities

* Receive sensor data
* Process camera input
* Run detection software
* Combine sensor information
* Calculate TTC
* Perform risk assessment
* Generate warnings
* Communicate with the monitoring interface

### Why It Is Used

A Raspberry Pi provides enough computing capability for a student prototype while keeping the system compact and portable.

### Connection

```text
Sensors / Camera
       ↓
Raspberry Pi
       ↓
Processing Software
       ↓
Warning System
```

---

# 4. Camera Module

### Purpose

The camera captures visual information from the road surrounding the vehicle.

The captured images can be processed by the computer-vision software to identify objects.

### Possible Detection Targets

* Mine vehicles
* Light vehicles
* People
* Obstacles
* Road-side objects

### Role in the System

```text
Camera
   ↓
Image Capture
   ↓
Computer Vision
   ↓
Object Detection
   ↓
Object Information
```

The camera provides visual information that can be combined with other sensor data.

---

# 5. IR / NIR Camera

### Purpose

An IR/NIR camera can provide additional information under low-light conditions.

This is useful because the SIH problem specifically involves situations where normal visibility is reduced.

### Possible Uses

* Low-light vehicle detection
* Object identification
* Supporting camera-based detection
* Additional visibility information

### Connection

```text
IR/NIR Camera
      ↓
Processing Unit
      ↓
Image Processing
      ↓
Object Detection
```

---

# 6. Ultrasonic Sensor

### Purpose

An ultrasonic sensor can be used in the small-scale prototype to measure the distance between the prototype vehicle and nearby objects.

It works by transmitting an ultrasonic signal and measuring the returning signal.

### Prototype Use

The sensor can be used for simple obstacle-distance testing.

```text
Ultrasonic Sensor
       ↓
Distance Measurement
       ↓
Processing Unit
       ↓
Risk Calculation
```

### Important Note

Ultrasonic sensing is mainly suitable for the prototype demonstration. For a real open-cast mine vehicle, longer-range sensing such as automotive-grade radar would be more appropriate.

---

# 7. 77 GHz mmWave Radar

### Purpose

A 77 GHz mmWave radar is proposed as a primary long-range sensing technology for the actual mine-vehicle application.

It can provide information about nearby objects and their relative movement.

### Possible Information

* Object distance
* Relative speed
* Direction of movement
* Object presence
* Relative position

### Role

```text
77 GHz Radar
      ↓
Object Information
      ↓
Sensor Fusion
      ↓
TTC Calculation
      ↓
Risk Assessment
```

### Prototype Status

**Proposed / Advanced Hardware**

The actual radar module should be added here once the team finalizes and tests the selected hardware.

---

# 8. GPS / GNSS Module

### Purpose

The GPS/GNSS module provides the location of the vehicle.

Location information is useful for recording where safety events occur.

### Possible Uses

* Vehicle position
* Route tracking
* Event location
* Near-miss location
* High-risk area identification

### Example

```text
GNSS
 ↓
Vehicle Coordinates
 ↓
Event Location
 ↓
Safety Database
 ↓
Risk Heatmap
```

---

# 9. MPU6050 IMU

### Purpose

The IMU provides information about vehicle movement and orientation.

The MPU6050 contains an accelerometer and gyroscope.

### Possible Information

* Acceleration
* Rotation
* Orientation changes
* Vehicle movement

### Role

IMU information can support vehicle-state estimation and sensor fusion.

```text
MPU6050
   ↓
Motion Data
   ↓
Processing Unit
   ↓
Vehicle State
```

---

# 10. Wheel Encoder

### Purpose

A wheel encoder can be used to measure wheel rotation.

The measured wheel rotation can be used to estimate:

* Vehicle speed
* Distance travelled
* Direction of movement

### Working Flow

```text
Wheel Rotation
      ↓
Encoder Pulses
      ↓
Microcontroller
      ↓
Speed Calculation
      ↓
Risk Assessment
```

---

# 11. Microcontroller

### Purpose

The microcontroller can be used for low-level hardware interfacing.

It can collect data from simple sensors and send the information to the main processing unit.

### Responsibilities

* Read sensor values
* Count encoder pulses
* Control LEDs
* Control buzzer
* Send sensor information
* Receive commands from the main processor

### Example Flow

```text
Sensors
   ↓
Microcontroller
   ↓
Serial / USB / Wireless Communication
   ↓
Raspberry Pi
```

The exact microcontroller should be changed to the board actually used by the team.

---

# 12. Buzzer

### Purpose

The buzzer provides an audio warning to the vehicle operator.

When the system detects a high-risk situation, the buzzer can be activated.

### Example

```text
Risk Level
    ↓
HIGH
    ↓
Buzzer Activated
    ↓
Operator Alert
```

Different warning patterns can be used for different risk levels if supported by the prototype.

---

# 13. LED Indicators

### Purpose

LEDs provide a simple visual indication of the current risk level.

Example:

```text
LOW       → Normal indication
MEDIUM    → Attention indication
HIGH      → Warning indication
CRITICAL  → Immediate warning indication
```

The exact LED behaviour should be configured according to the implemented prototype.

---

# 14. OLED / LCD Display

### Purpose

A small display can provide important information directly to the operator or during prototype demonstration.

### Possible Display Information

```text
Vehicle Speed: 22 km/h
Object Distance: 28 m
TTC: 4.2 sec
Risk: HIGH
Warning: REDUCE SPEED
```

### Role

```text
Risk Assessment
       ↓
Display Controller
       ↓
OLED / LCD
       ↓
Operator
```

---

# 15. V2V Communication Module

### Purpose

Vehicle-to-vehicle communication can allow nearby vehicles to exchange safety-related information.

### Possible Information

* Vehicle ID
* Position
* Speed
* Heading
* Safety status

### Example

```text
Vehicle A
    │
    │ V2V
    ▼
Vehicle B
```

The received information can be processed together with local sensor data.

### Prototype Status

**Proposed / Future Extension**, unless a V2V communication module is already included in the prototype.

---

# 16. Power Supply / Battery

### Purpose

The power system supplies the required electrical power to the sensors, processing unit and output devices.

### Requirements

The power supply should provide suitable voltage and current for each component.

```text
Battery / Power Supply
          │
          ▼
   Power Distribution
     ┌────┼────┐
     ▼    ▼    ▼
 Sensors  Pi  Outputs
```

Voltage requirements should be checked against the datasheets of the actual components before connecting them.

---

# 17. Breadboard / Prototype Board

### Purpose

A breadboard or prototype board can be used to assemble and test the electronic connections during development.

It allows the team to:

* Connect sensors
* Test circuits
* Change connections easily
* Debug hardware
* Test warning outputs

For a final rugged system, proper connectors and secured wiring should replace temporary breadboard connections.

---

# 18. Jumper Wires and Connectors

### Purpose

Jumper wires and connectors are used to connect the sensors, microcontroller, processing unit and output devices during prototype development.

They are mainly used for:

* Power connections
* Ground connections
* Signal connections
* Communication connections

All connections should be checked before powering the system.

---

# 19. Vehicle Prototype Chassis

### Purpose

A small vehicle chassis can be used to demonstrate the proposed mine-vehicle safety system.

The prototype can represent a mine vehicle during testing.

Possible mounting areas include:

```text
              FRONT
                ↑
        ┌───────────────┐
        │ Camera        │
        │ Radar/Sensor  │
        │               │
        │ Processing    │
        │ Unit          │
        │               │
        │ Battery       │
        └───────────────┘
              WHEELS
```

The final sensor placement depends on the actual prototype design.

---

# 20. Hardware Integration

The major components work together as follows:

```text
                  ┌──────────────┐
                  │    CAMERA    │
                  └──────┬───────┘
                         │
                  ┌──────▼───────┐
                  │    RADAR     │
                  └──────┬───────┘
                         │
                  ┌──────▼───────┐
                  │   GNSS/IMU   │
                  └──────┬───────┘
                         │
                  ┌──────▼───────┐
                  │ WHEEL ENCODER│
                  └──────┬───────┘
                         │
                         ▼
               ┌──────────────────┐
               │ MICROCONTROLLER  │
               └────────┬─────────┘
                        │
                        ▼
               ┌──────────────────┐
               │  RASPBERRY PI    │
               │ PROCESSING UNIT  │
               └────────┬─────────┘
                        │
                        ▼
               ┌──────────────────┐
               │ SENSOR FUSION    │
               └────────┬─────────┘
                        │
                        ▼
               ┌──────────────────┐
               │ TTC + RISK       │
               │ ASSESSMENT       │
               └────────┬─────────┘
                        │
                 ┌──────┴──────┐
                 ▼             ▼
              BUZZER        DISPLAY
                 │             │
                 └──────┬──────┘
                        ▼
                    OPERATOR
```

---

# 21. Hardware-to-Software Interaction

The hardware continuously provides information to the software.

```text
Hardware
   ↓
Sensor Data
   ↓
Data Acquisition
   ↓
Data Processing
   ↓
Sensor Fusion
   ↓
Object Detection
   ↓
TTC Calculation
   ↓
Risk Assessment
   ↓
Warning
```

This allows the system to connect physical sensing with the software decision-support layer.

---

# 22. Component Selection Considerations

The hardware components are selected based on factors such as:

* Detection range
* Low-visibility performance
* Processing requirements
* Power consumption
* Communication capability
* Cost
* Prototype availability
* Ease of integration
* Reliability
* Suitability for mine environments

For an actual mining deployment, industrial-grade and ruggedized hardware would be required.

---

# 23. Prototype vs Real Mine Deployment

The hardware used in a student prototype may be smaller and less rugged than the hardware required for an actual mine vehicle.

| Prototype            | Real Mine Deployment                     |
| -------------------- | ---------------------------------------- |
| Small camera         | Industrial camera                        |
| Ultrasonic sensor    | Long-range automotive/industrial radar   |
| Raspberry Pi         | Industrial/automotive computing platform |
| Small GPS module     | Industrial GNSS                          |
| Breadboard           | Rugged wiring/connectors                 |
| Small battery        | Vehicle power system                     |
| Small buzzer/display | Vehicle-grade warning interface          |

The prototype is intended to demonstrate the core concept and workflow. Real-world deployment would require additional environmental, electrical, mechanical and safety validation.

---

# 24. Hardware Status

### Core Prototype Components

Add only components that are actually available and connected in the current prototype.

```text
- Raspberry Pi / Processing Unit
- Camera
- Microcontroller
- Distance Sensor
- GNSS
- IMU
- Buzzer
- LED / Display
- Power Supply
```

### Proposed Components

The following can be added as the project develops:

```text
- 77 GHz mmWave Radar
- LWIR Thermal Camera
- V2V Communication
- Industrial GNSS
- Ruggedized processing hardware
```

---

# 25. Summary

The hardware system provides the physical sensing and output layer of the SIH26007 solution.

The sensors collect information about the vehicle and its surroundings. The processing unit receives this information and passes it to the software for sensor fusion, object tracking, TTC calculation and risk assessment.

The final warning is provided through suitable visual or audio outputs.

```text
SENSORS
   ↓
DATA COLLECTION
   ↓
PROCESSING UNIT
   ↓
SENSOR FUSION
   ↓
RISK ASSESSMENT
   ↓
WARNING
   ↓
VEHICLE OPERATOR
```

The overall hardware design is intended to support safer vehicle operation in fog and low-visibility conditions in open-cast iron ore mines.
