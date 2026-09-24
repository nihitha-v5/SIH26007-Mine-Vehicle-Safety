# Hardware Connections

## 1. Overview

The hardware system is designed to collect information about the mine vehicle, nearby vehicles, obstacles, and visibility conditions.

The sensor data is sent to the processing unit, where it is combined and used for collision-risk assessment. Based on the calculated risk, the system can generate a warning for the vehicle operator.

### Basic Connection Flow

```text
                    MINE VEHICLE
                         │
                         ▼
              ┌─────────────────────┐
              │   SENSING SYSTEM    │
              └──────────┬──────────┘
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
      Radar           Camera        Vehicle Sensors
        │                │          GNSS / IMU /
        │                │          Wheel Odometry
        │                │                │
        └────────────────┼────────────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │ PROCESSING UNIT     │
              │ / EDGE CONTROLLER   │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │ SENSOR FUSION &     │
              │ RISK ASSESSMENT     │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │ WARNING / DISPLAY   │
              └──────────┬──────────┘
                         │
                         ▼
                  VEHICLE OPERATOR
```

---

## 2. Sensor Connections

The proposed system uses multiple sensing sources because a single sensor may not provide reliable information in fog and low-visibility conditions.

| Input                          | Connected To        | Purpose                                                            |
| ------------------------------ | ------------------- | ------------------------------------------------------------------ |
| 77 GHz mmWave Radar            | Processing Unit     | Detect nearby objects, distance and relative movement              |
| IR/NIR Camera                  | Processing Unit     | Detect vehicles, people and obstacles in reduced visibility        |
| LWIR Thermal Camera (optional) | Processing Unit     | Provide additional information during darkness and poor visibility |
| GNSS                           | Processing Unit     | Vehicle position and location                                      |
| IMU                            | Processing Unit     | Vehicle acceleration, orientation and movement                     |
| Wheel Odometry                 | Processing Unit     | Vehicle speed and travelled distance                               |
| V2V Communication              | Processing Unit     | Exchange information with nearby vehicles                          |
| Mine Map Data                  | Processing Software | Provide road geometry and restricted/high-risk areas               |

---

## 3. Processing Unit

The processing unit acts as the main point for collecting and processing the sensor information.

It receives data from:

* Radar
* Camera
* GNSS
* IMU
* Wheel odometry
* V2V communication

The processing unit then passes the collected information to the sensor-fusion and risk-assessment software.

### Processing Flow

```text
Sensor Inputs
     │
     ▼
Data Collection
     │
     ▼
Data Synchronization
     │
     ▼
Sensor Fusion
     │
     ▼
Object / Vehicle Information
     │
     ▼
TTC + Risk Assessment
     │
     ▼
Warning Generation
```

---

## 4. Communication Connections

The system may use communication between nearby mine vehicles to improve awareness beyond the sensors mounted on a single vehicle.

```text
        VEHICLE A
     ┌─────────────┐
     │ Sensors     │
     │ Processing  │
     └──────┬──────┘
            │
            │ V2V
            │ Communication
            ▼
     ┌─────────────┐
     │   VEHICLE B │
     │ Sensors     │
     │ Processing  │
     └─────────────┘
```

The exchanged information can include:

* Vehicle position
* Vehicle speed
* Vehicle heading
* Vehicle identification
* Safety-related status

---

## 5. Warning Output Connections

After the risk is assessed, the system sends the warning information to the operator.

```text
Risk Assessment
       │
       ▼
Warning Decision
       │
   ┌───┴────┐
   │        │
   ▼        ▼
Display    Audio
Warning    Warning
   │        │
   └───┬────┘
       ▼
Vehicle Operator
```

Possible warning outputs include:

* Dashboard display
* Audio warning
* Visual warning indicator
* HUD (if included in the prototype)

---

## 6. Overall Hardware Connection

```text
 ┌─────────────┐
 │  77 GHz     │
 │ Radar       │
 └──────┬──────┘
        │
 ┌──────▼──────┐
 │ IR/NIR      │
 │ Camera      │
 └──────┬──────┘
        │
 ┌──────▼──────┐
 │ GNSS + IMU  │
 └──────┬──────┘
        │
 ┌──────▼──────┐
 │ Wheel       │
 │ Odometry    │
 └──────┬──────┘
        │
 ┌──────▼──────┐
 │ V2V         │
 │ Communication│
 └──────┬──────┘
        │
        ▼
┌──────────────────────┐
│    PROCESSING UNIT   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ SENSOR FUSION        │
│ + OBJECT TRACKING    │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ TTC + RISK           │
│ ASSESSMENT           │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ WARNING / DISPLAY    │
└──────────┬───────────┘
           │
           ▼
    VEHICLE OPERATOR
```

---

## 7. Connection Notes

* All sensors should be securely mounted on the vehicle/prototype.
* Sensor data should be synchronized before sensor fusion.
* The processing unit acts as the central point for collecting sensor information.
* Communication interfaces depend on the actual hardware selected for the prototype.
* Warning devices should be placed where the operator can easily notice them.
* Final wiring and pin connections should follow the datasheets of the actual components used.

## 8. Prototype Status

The exact physical connections depend on the hardware available in the prototype.

The architecture described above represents the proposed connection structure for the SIH26007 solution. Actual component names, interfaces, pin numbers and wiring should be added after the final hardware setup is completed.
