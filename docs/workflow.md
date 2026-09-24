# System Workflow

The system works in a continuous cycle: it collects information from the mine vehicle and its surroundings, understands the current situation, predicts possible danger, warns the operator, and stores important safety events for future analysis.

## 1. Data Collection

The system collects real-time information from multiple sources:

* **77 GHz mmWave Radar** – detects distance and relative movement of nearby objects.
* **IR/NIR Camera** – helps identify vehicles, people, and obstacles in reduced visibility.
* **GNSS** – provides vehicle location.
* **IMU** – provides movement and heading information.
* **Wheel Odometry** – provides vehicle speed and movement.
* **V2V Communication** – provides information shared by nearby connected vehicles.
* **Digital Mine Map** – provides road and mine-area information.

```text
Radar + Camera + GNSS + IMU + Odometry + V2V
                         ↓
                  Real-Time Data
```

## 2. Data Synchronization

Data from different sensors arrives at different times and speeds.

The system synchronizes the incoming data so that information from different sources can be processed together.

```text
Different Sensor Data
          ↓
   Synchronization
          ↓
   Aligned Data
```

## 3. Sensor Fusion

The synchronized data is combined to create a common understanding of the vehicle's surroundings.

For example, radar provides distance while the camera helps identify the object. Combining both gives more useful information than relying on only one source.

```text
Radar ───────┐
Camera ──────┤
GNSS ────────┤
IMU ─────────┼──→ SENSOR FUSION
Odometry ────┤
V2V ─────────┘
                  ↓
        Common Situation Picture
```

## 4. Object Detection and Tracking

The system identifies relevant objects such as:

* Heavy vehicles
* Light vehicles
* Workers
* Obstacles
* Other potential hazards

After detection, the system continuously tracks their:

* Position
* Distance
* Speed
* Direction
* Relative movement

This helps determine whether an object is moving towards, away from, or across the vehicle's path.

## 5. Movement Prediction

The system uses the current vehicle and object information to estimate their future movement.

Prediction considers factors such as:

* Position
* Speed
* Heading
* Relative movement
* Distance
* Road geometry
* Vehicle type
* Visibility conditions

This helps identify situations where two vehicles may enter the same path.

## 6. Time to Collision (TTC)

When vehicles or objects are approaching each other, the system estimates the **Time to Collision (TTC)**.

```text
TTC = Distance / Closing Speed
```

Example:

```text
Distance = 30 m
Closing Speed = 10 m/s

TTC = 30 / 10
    = 3 seconds
```

A lower TTC indicates that the situation may require more immediate attention.

## 7. Dynamic Risk Assessment

The system does not depend only on distance or TTC. It considers multiple factors together:

* Distance
* Relative speed
* TTC
* Vehicle type
* Visibility
* Road geometry
* Vehicle speed
* Traffic conditions

The current situation is then assigned an appropriate risk level.

```text
Sensor Information
        ↓
Movement + TTC
        ↓
Risk Factors
        ↓
Collision Risk
```

## 8. Risk-Prioritized Warning

If a potentially dangerous situation is detected, the system provides a warning to the operator.

The warning can include:

* Risk level
* Direction of hazard
* Distance
* TTC
* Suggested action

Example:

```text
⚠ HIGH RISK

Vehicle approaching from left
Distance: 28 m
TTC: 4.2 seconds

Action: Reduce Speed
```

The warning priority changes according to the severity of the situation.

## 9. Near-Miss Detection

The system can identify situations where a serious collision risk occurs but a collision is avoided.

Example:

```text
Vehicle approaches
       ↓
TTC becomes low
       ↓
Operator reduces speed
       ↓
Collision avoided
       ↓
Near-Miss Recorded
```

Near-miss information is important because repeated near-misses can indicate unsafe areas or traffic patterns.

## 10. Event Storage

Important safety events are stored for further analysis.

The system can record:

* Date and time
* Vehicle location
* Object type
* Distance
* Speed
* TTC
* Visibility condition
* Risk level
* Warning generated
* Near-miss information

## 11. Risk Analysis and High-Risk Locations

Stored events are analyzed to identify repeated dangerous situations.

```text
Safety Events
      ↓
Risk Analysis
      ↓
Repeated Near-Misses
      ↓
High-Risk Locations
      ↓
Risk Heatmap
```

This helps identify road sections, turns, intersections, or other locations where additional safety measures may be needed.

## 12. Continuous Safety Improvement

The system uses historical safety events to understand recurring patterns.

This can help mine operators identify:

* Frequently occurring near-misses
* Repeated warning locations
* Risky road sections
* Visibility-related risks
* Traffic-related safety patterns

The information can support preventive safety planning and improve the overall operation of mine vehicles.

---

## Complete System Workflow

```text
┌──────────────────────────────┐
│     SENSOR & VEHICLE DATA    │
│ Radar | Camera | GNSS | IMU  │
│ Odometry | V2V | Mine Map    │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│      DATA SYNCHRONIZATION    │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│        SENSOR FUSION         │
│   Common Situation Picture   │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│   OBJECT DETECTION & TRACKING│
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│     MOVEMENT PREDICTION      │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│       TTC CALCULATION        │
│  TTC = Distance / Closing    │
│           Speed              │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│      DYNAMIC RISK ASSESSMENT │
└──────────────┬───────────────┘
               ↓
       ┌───────┴────────┐
       ↓                ↓
   LOW / SAFE       HIGH RISK
                        ↓
              ┌─────────────────┐
              │ WARNING SYSTEM  │
              └────────┬────────┘
                       ↓
                VEHICLE OPERATOR
                       ↓
              SAFETY EVENT LOG
                       ↓
                RISK ANALYSIS
                       ↓
                 RISK HEATMAP
```

### Overall Flow

**Collect → Synchronize → Fuse → Detect → Track → Predict → Calculate TTC → Assess Risk → Warn → Record → Analyze → Improve Safety**
