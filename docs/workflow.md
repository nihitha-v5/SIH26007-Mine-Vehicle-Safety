# System Workflow

The system works through the following sequence:

1. Collect Data
       ↓
2. Synchronize Inputs
       ↓
3. Sensor Fusion
       ↓
4. Detect Objects
       ↓
5. Track Movement
       ↓
6. Predict Trajectory
       ↓
7. Calculate TTC
       ↓
8. Assess Collision Risk
       ↓
9. Generate Warning
       ↓
10. Store Safety Event
       ↓
11. Update Risk Information
```

## Step 1 – Collect Data

Information is collected from the available sensors, vehicle systems, V2V communication and mine-map data.

## Step 2 – Synchronize Inputs

Data from different sources is brought together so that it can be processed as a common situation.

## Step 3 – Sensor Fusion

The system combines the available information to improve the understanding of the surroundings.

## Step 4 – Object Detection

Nearby vehicles, people or obstacles are identified using the available sensing inputs.

## Step 5 – Movement Tracking

The system observes how detected objects are moving relative to the mine vehicle.

## Step 6 – Trajectory Prediction

The system estimates possible future movement based on position, speed, heading, road geometry and other available information.

## Step 7 – TTC Calculation

Time to Collision is estimated using distance and relative closing speed where applicable.

## Step 8 – Risk Assessment

The system combines TTC with other factors such as visibility, vehicle type, distance, traffic and road conditions.

## Step 9 – Warning

An appropriate warning is provided to the operator based on the calculated risk.

## Step 10 – Event Storage

Important events such as near misses and repeated warnings can be stored.

## Step 11 – Risk Information

Repeated events can be analysed to identify high-risk areas and support preventive action.
