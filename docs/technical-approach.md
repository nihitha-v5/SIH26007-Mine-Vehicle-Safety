# Technical Approach

Our proposed system follows a six-stage approach:

**SENSE → FUSE → PREDICT → ASSESS → ADVISE → LEARN**

The main idea is to collect information from different sources, combine it to understand the current situation, predict possible risks, provide the right warning to the driver, and learn from previous safety events.

---

## 1. SENSE — Collect Real-Time Data

The first stage is to collect real-time information about the mine vehicle and its surroundings.

Instead of depending on a single sensor, the system uses multiple sensing inputs so that the limitations of one sensor can be compensated for by information from other sources.

### Sensing Inputs

* **77 GHz mmWave Radar** → Provides distance, relative motion and obstacle information.
* **IR/NIR Camera** → Helps detect vehicles, people and obstacles in reduced-visibility conditions.
* **Optional LWIR Thermal Camera** → Provides additional information in darkness and fog.
* **GNSS + IMU + Wheel Odometry** → Provides vehicle position, speed, heading and movement information.
* **V2V Communication** → Provides information such as position, speed and heading of nearby vehicles.
* **Digital Mine Map** → Provides road geometry, turns, road edges and restricted-zone information.
* **HUD** → Can be used to display important warnings and information to the driver.

These inputs form the sensing layer of the system.

---

## 2. FUSE — Build a Common Situation Picture

The information collected from different sources is synchronized and combined using a **Sensor Fusion Engine**.

The purpose of sensor fusion is to bring different types of information together and create a common picture of what is happening around the vehicle.

```text
77 GHz Radar ─────┐
IR/NIR Camera ────┤
GNSS ─────────────┤
IMU ──────────────┤
Wheel Odometry ───┤
V2V ──────────────┤ → SENSOR FUSION → SITUATIONAL AWARENESS
Mine Map ─────────┘
```

The output of this stage is a better understanding of the vehicle's surroundings, including nearby objects, their movement and the road situation.

---

## 3. PREDICT — Predict Possible Future Situations

After understanding the current situation, the system estimates how the vehicle and nearby objects may move in the near future.

### 3.1 Trajectory Prediction

The trajectory-prediction stage can use information such as:

* Own vehicle position
* Own vehicle speed
* Own vehicle heading
* Object position
* Object speed
* Object heading
* Distance between vehicles
* Road geometry
* Vehicle type
* Visibility conditions
* Relative movement

Using these inputs, the system estimates the possible future trajectory of the vehicle and nearby objects.

---

### 3.2 Time to Collision (TTC)

**Time to Collision (TTC)** is the estimated time remaining before two objects could collide if their current relative motion continues.

For a simple closing-speed situation:

```text
TTC = Distance / Closing Speed
```

### Example

```text
Distance = 30 m
Closing Speed = 10 m/s

TTC = 30 / 10
    = 3 seconds
```

So, under the given conditions, the estimated time before collision is approximately **3 seconds** if the current relative motion continues.

The estimated visibility can also be considered while calculating collision risk and deciding how the warning strategy should respond.

---

### 3.3 Near-Miss Detection and Learning

Not every dangerous situation results in a collision. A **near miss** is a situation where a possible collision occurs but is avoided.

For example:

A truck is travelling at 20 km/h and a light vehicle suddenly crosses its path. The estimated TTC falls to 1.8 seconds. The truck slows down and the collision is avoided.

The system can record this event instead of simply ignoring it.

If similar near-miss events occur repeatedly at the same location, that location can be identified as a **high-risk zone** on the mine map.

In the future, when another vehicle approaches the same area, the system can provide an earlier warning.

---

## 4. ASSESS — Calculate Dynamic Collision Risk

The system does not stop at detecting an object.

It also evaluates how risky the current situation is.

The risk assessment can consider factors such as:

* Distance
* Relative speed
* Time to Collision (TTC)
* Vehicle type
* Visibility
* Road geometry
* Truck speed
* Traffic conditions

### Example

```text
Distance      = 60 m
TTC           = 15 seconds
Visibility    = 100 m
Road          = Straight
Traffic       = Low
```

Based on these conditions, the situation may be classified as **LOW RISK**.

As the vehicle moves, these values can change. The risk level can therefore be updated dynamically instead of remaining fixed.

---

## 5. ADVISE — Give the Right Warning

The ADVISE stage converts the calculated risk into a warning that the driver can understand and respond to quickly.

The system provides **risk-prioritized alerts** instead of giving the same warning for every detected object.

### Example

```text
⚠ HIGH RISK

Vehicle approaching from left

Distance: 28 m
TTC: 4.2 seconds

Action: Reduce speed
```

### Possible Warning Outputs

* Audio warning
* Dashboard display
* Optional HUD
* Recommended speed
* Direction of the hazard
* Location of the hazard

The warning can be based on the severity of the situation, allowing the driver to focus on the most important hazards first.

---

## 6. LEARN — Improve Safety Over Time

The system can store important safety-related events and conditions for further analysis.

The information that can be stored includes:

* Collision events
* Near-miss events
* Repeated warnings
* High-risk locations
* Visibility conditions
* Traffic patterns

The stored information can be used to identify areas and situations where risky events occur repeatedly.

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

This allows the system to go beyond giving an immediate warning and support long-term safety improvements in mine operations.

---

## Overall Approach

The complete approach can be summarized as:

```text
SENSE
Collect real-time sensor and vehicle data
        ↓
FUSE
Combine the information into a common situation picture
        ↓
PREDICT
Predict movement and estimate Time to Collision
        ↓
ASSESS
Calculate the current collision risk
        ↓
ADVISE
Give the driver a risk-prioritized warning
        ↓
LEARN
Store events and identify repeated high-risk locations

The overall goal is to provide the mine vehicle operator with better situational awareness and timely information during fog and other low-visibility conditions.
