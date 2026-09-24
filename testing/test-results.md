# Testing and Test Results

## 1. Purpose of Testing

Testing is performed to check whether the proposed mine-vehicle safety system can correctly collect sensor information, identify nearby objects, estimate collision risk, and provide timely warnings under different operating conditions.

The system is tested under normal visibility as well as reduced-visibility conditions such as fog, dust, darkness, and obstructed visibility.

---

## 2. Testing Approach

Testing is divided into different stages:

1. Hardware Testing
2. Sensor Testing
3. Data Collection Testing
4. Object Detection Testing
5. Object Tracking Testing
6. TTC Calculation Testing
7. Risk Assessment Testing
8. Warning System Testing
9. Near-Miss Testing
10. End-to-End System Testing

---

# 3. Hardware Testing

Each hardware component is checked individually before integrating the complete system.

| Component       | Test Performed             | Expected Result                   | Status       |
| --------------- | -------------------------- | --------------------------------- | ------------ |
| Radar           | Detect nearby object       | Object distance/movement received | To be filled |
| Camera          | Capture surroundings       | Clear image/frame received        | To be filled |
| GNSS            | Check vehicle position     | Location received correctly       | To be filled |
| IMU             | Check movement and heading | Motion data received              | To be filled |
| Wheel Encoder   | Check wheel movement       | Speed/distance data received      | To be filled |
| Buzzer          | Trigger warning            | Audible alert generated           | To be filled |
| Display         | Show warning               | Warning information displayed     | To be filled |
| Processing Unit | Process sensor inputs      | Data processed correctly          | To be filled |

---

# 4. Sensor Testing

Individual sensors are tested to verify whether they provide useful information to the processing system.

### Radar Test

The radar is tested by placing objects at different distances.

```text
Radar
  ↓
Object Detection
  ↓
Distance Measurement
  ↓
Movement Information
```

The received distance and movement information are compared with the actual test conditions.

### Camera Test

The camera is tested under:

* Normal lighting
* Low lighting
* Reduced visibility
* Different object distances

The purpose is to check whether relevant objects can be identified.

### GNSS Test

GNSS data is checked to verify:

* Vehicle position
* Location updates
* Position availability

### IMU Test

The IMU is tested during different vehicle movements such as:

* Forward movement
* Turning
* Stopping
* Direction changes

### Wheel Odometry Test

Wheel movement is monitored to estimate:

* Vehicle speed
* Distance travelled
* Movement state

---

# 5. Normal Visibility Testing

The system is first tested under normal visibility conditions.

### Test Scenario

A mine vehicle moves on a clear road while another vehicle is present at a safe distance.

### Expected Behaviour

* Nearby vehicle should be detected.
* Distance should be monitored.
* Vehicle movement should be tracked.
* TTC should be calculated when applicable.
* No unnecessary high-risk warning should be generated.

### Result

**To be filled after physical testing.**

---

# 6. Low-Visibility Testing

The system is tested under conditions representing reduced visibility.

Examples include:

* Fog
* Dust
* Low light
* Partial obstruction

### Expected Behaviour

The system should continue using available sensor information and identify relevant nearby objects as reliably as possible.

The system should also consider visibility conditions during risk assessment.

### Result

**To be filled after physical testing.**

---

# 7. Approaching Vehicle Test

### Scenario

Another vehicle approaches the mine vehicle from the front.

```text
        Vehicle A
             ↓
             ↓
        ← approaching →
             ↓
        Vehicle B
```

### Expected Behaviour

The system should:

1. Detect the approaching vehicle.
2. Measure the distance.
3. Track its movement.
4. Calculate closing speed.
5. Estimate TTC.
6. Assess the collision risk.
7. Generate a warning if the risk becomes significant.

### Result

**To be filled after testing.**

---

# 8. Crossing Vehicle Test

### Scenario

A vehicle crosses the path of the mine vehicle.

### Expected Behaviour

The system should identify the crossing movement and determine whether the two vehicle paths may create a collision risk.

If the risk becomes significant, an appropriate warning should be generated.

### Result

**To be filled after testing.**

---

# 9. TTC Calculation Testing

The TTC module is tested using known distance and closing-speed values.

### Formula

```text
TTC = Distance / Closing Speed
```

### Example Test

```text
Distance = 30 m
Closing Speed = 10 m/s

Expected TTC = 3 seconds
```

The calculated value from the system is compared with the expected value.

| Distance | Closing Speed | Expected TTC |   System TTC | Status       |
| -------: | ------------: | -----------: | -----------: | ------------ |
|     30 m |        10 m/s |        3 sec | To be filled | To be filled |
|     50 m |         5 m/s |       10 sec | To be filled | To be filled |
|     20 m |        10 m/s |        2 sec | To be filled | To be filled |

---

# 10. Risk Assessment Testing

Different situations are created to check whether the risk assessment responds appropriately.

| Situation                                   | Distance |    TTC | Visibility | Expected Risk |
| ------------------------------------------- | -------: | -----: | ---------- | ------------- |
| Safe vehicle                                |     High |   High | Good       | Low           |
| Approaching vehicle                         |   Medium | Medium | Good       | Medium        |
| Fast approaching vehicle                    |      Low |    Low | Good       | High          |
| Approaching vehicle in poor visibility      |      Low |    Low | Poor       | High          |
| Crossing vehicle with sufficient separation |   Medium |   High | Good       | Low/Medium    |

**Actual system results should be entered after testing.**

---

# 11. Warning System Testing

The warning system is tested to verify that alerts are generated when required.

### Warning Levels

```text
LOW RISK
   ↓
Normal Monitoring

MEDIUM RISK
   ↓
Caution Warning

HIGH RISK
   ↓
Immediate Warning
```

### Warning Test

The system is checked for:

* Correct warning level
* Correct hazard direction
* Distance information
* TTC information
* Recommended action
* Audio/visual alert generation

### Example

```text
⚠ HIGH RISK

Vehicle approaching from left
Distance: 28 m
TTC: 4.2 seconds

Action: Reduce Speed
```

---

# 12. Near-Miss Testing

A near-miss scenario is created where the collision risk becomes high but the vehicles avoid a collision.

```text
Vehicle Approaches
        ↓
TTC Decreases
        ↓
High Risk Detected
        ↓
Warning Generated
        ↓
Vehicle Slows / Situation Changes
        ↓
Collision Avoided
        ↓
Near-Miss Recorded
```

The system should record the event for later analysis.

### Result

**To be filled after testing.**

---

# 13. High-Risk Location Testing

Multiple safety events can be recorded at different locations.

The stored data is analyzed to identify locations where risky situations occur repeatedly.

```text
Safety Events
      ↓
Location Analysis
      ↓
Repeated Events
      ↓
High-Risk Location
      ↓
Risk Heatmap
```

This information can help identify areas where additional safety measures may be required.

---

# 14. End-to-End Testing

The complete system is tested as one integrated unit.

### Test Flow

```text
Sensors
   ↓
Data Collection
   ↓
Synchronization
   ↓
Sensor Fusion
   ↓
Object Detection
   ↓
Object Tracking
   ↓
Movement Prediction
   ↓
TTC Calculation
   ↓
Risk Assessment
   ↓
Warning
   ↓
Event Storage
   ↓
Risk Analysis
```

The purpose of this test is to verify that all major modules work together correctly.

---

# 15. Test Case Summary

| Test ID | Test Case           | Expected Outcome                     | Actual Result | Status  |
| ------- | ------------------- | ------------------------------------ | ------------- | ------- |
| T01     | Hardware startup    | All connected components initialize  | To be filled  | Pending |
| T02     | Radar detection     | Nearby object detected               | To be filled  | Pending |
| T03     | Camera detection    | Relevant object identified           | To be filled  | Pending |
| T04     | GNSS data           | Vehicle position received            | To be filled  | Pending |
| T05     | IMU data            | Movement information received        | To be filled  | Pending |
| T06     | Object tracking     | Object movement tracked              | To be filled  | Pending |
| T07     | TTC calculation     | Correct TTC calculated               | To be filled  | Pending |
| T08     | Risk assessment     | Appropriate risk level generated     | To be filled  | Pending |
| T09     | Warning generation  | Warning generated when required      | To be filled  | Pending |
| T10     | Near-miss detection | Near-miss recorded                   | To be filled  | Pending |
| T11     | Event storage       | Safety event stored                  | To be filled  | Pending |
| T12     | Risk analysis       | High-risk location identified        | To be filled  | Pending |
| T13     | End-to-end test     | Complete workflow operates correctly | To be filled  | Pending |

---

# 16. Testing Evidence

Actual testing evidence should be added to the repository.

Recommended evidence:

```text
testing/
│
├── test-results.md
├── screenshots/
│   ├── sensor-output.png
│   ├── object-detection.png
│   ├── ttc-calculation.png
│   ├── warning-output.png
│   └── dashboard-output.png
│
└── videos/
    └── prototype-test.mp4
```

For hardware testing, add actual photographs of the prototype during testing.

For software testing, add screenshots of the actual system output.

---

# 17. Performance Metrics

After sufficient testing, the following metrics can be recorded:

* Object detection accuracy
* Object tracking accuracy
* TTC calculation accuracy
* Warning response time
* Sensor data processing time
* False warning rate
* Missed detection rate
* System uptime
* Detection performance under reduced visibility

Only measured values should be added to the final report.

---

# 18. Limitations During Testing

The prototype may have limitations depending on the available hardware, sensors, dataset, and testing environment.

Possible limitations include:

* Limited real-world mine testing
* Small prototype scale
* Limited low-visibility test conditions
* Limited number of vehicles
* Sensor range limitations
* Limited training data
* Differences between prototype conditions and actual mine environments

These limitations should be clearly mentioned instead of presenting estimated values as final results.

---

# 19. Final Testing Goal

The main goal of testing is to verify that the system can:

**Detect → Understand → Predict → Assess → Warn → Record**

under different mine-vehicle operating conditions.

The final testing results will be updated after physical prototype testing and software validation.

