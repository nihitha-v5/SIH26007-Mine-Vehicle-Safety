# System Architecture

## Overall Architecture

The proposed system collects information from different sensing and vehicle-data sources and combines them to create a common understanding of the mine vehicle's surroundings.

```text
                   MINE VEHICLE
                        │
                        ▼
              ┌──────────────────┐
              │  SENSING LAYER   │
              └────────┬─────────┘
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
      Radar         Camera       Vehicle Data
        │              │              │
        │              │       GNSS / IMU /
        │              │       Wheel Odometry
        │              │              │
        └──────────────┼──────────────┘
                       │
                       ▼
              ┌──────────────────┐
              │  SENSOR FUSION   │
              └────────┬─────────┘
                       │
                       ▼
              Situational Awareness
                       │
                       ▼
              ┌──────────────────┐
              │    PREDICTION    │
              └────────┬─────────┘
                       │
                  Trajectory
                   + TTC
                       │
                       ▼
              ┌──────────────────┐
              │  RISK ASSESSMENT │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │  WARNING SYSTEM  │
              └────────┬─────────┘
                       │
                       ▼
                 VEHICLE OPERATOR
                       │
                       ▼
                 EVENT STORAGE
                       │
                       ▼
                 RISK ANALYSIS
                       │
                       ▼
                 RISK HEATMAP
```

## Main Layers

### 1. Sensing Layer

Collects information about the surroundings and the vehicle itself.

### 2. Sensor Fusion Layer

Combines information from different sources to create a common situation picture.

### 3. Prediction Layer

Uses the current state of the vehicle and surrounding objects to estimate future movement.

### 4. Risk Assessment Layer

Evaluates the possibility and severity of a collision using multiple parameters.

### 5. Warning Layer

Converts the risk assessment into information that can be understood by the operator.

### 6. Learning and Data Layer

Stores important events and uses historical information to identify repeated risk locations and patterns.
