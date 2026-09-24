# SIH26007 – Problem Statement

## Safe and Efficient Operation of Mine Vehicles in Fog and Low-Visibility Conditions in Open Cast Iron Ore Mines

## 1. Introduction

Open-cast iron ore mines use large vehicles such as haul trucks, dump trucks, loaders and other heavy machinery for transporting and handling materials.

These vehicles operate on large mine roads and often work continuously in changing environmental conditions. Fog, dust, darkness and other low-visibility conditions can make it difficult for operators to clearly see nearby vehicles, people, obstacles and changes in the road.

In such situations, the operator may have less time to understand what is happening around the vehicle and respond to a potential hazard.

The problem is therefore to improve the operator's awareness of the surroundings and provide timely safety information during fog and low-visibility conditions.

---

## 2. Problem

During fog and reduced-visibility conditions in open-cast iron ore mines, vehicle operators may face difficulty in:

* Identifying nearby vehicles from a safe distance
* Detecting obstacles on the road
* Understanding the movement of approaching vehicles
* Judging the distance between vehicles
* Responding quickly to changing traffic situations
* Identifying hazards around turns and intersections
* Maintaining safe movement when visibility is poor

Large mining vehicles also have limitations in terms of visibility around the vehicle. This makes it important to provide additional information about the surrounding environment.

---

## 3. Why This Is a Safety Concern

A mine vehicle may be moving at a considerable speed while visibility is reduced.

For example, an operator may detect another vehicle only after it has entered a relatively short visible range. If the vehicles are already moving towards each other, the available reaction time can become limited.

The situation becomes more difficult when:

* Fog is dense
* Dust is present
* Lighting conditions are poor
* Roads contain sharp turns
* Multiple vehicles are operating together
* Vehicles have different sizes and speeds
* The operator cannot clearly see beyond the immediate surroundings

Therefore, relying only on direct visual observation may not provide sufficient situational information in every condition.

---

## 4. Existing Challenge

Traditional vehicle operation mainly depends on:

* Driver visibility
* Vehicle lights
* Mirrors
* Manual observation
* Existing communication systems

These methods may not provide a complete picture of nearby vehicle movement during severe low-visibility conditions.

The system needs to provide additional information that can help the operator understand:

* What objects are nearby
* Where they are located
* How they are moving
* How quickly they are approaching
* Whether the current situation requires attention

---

## 5. Need for a Solution

A safety-support system is needed that can continuously observe the vehicle's surroundings and provide useful information to the operator.

The solution should be able to make use of different sources of information rather than depending on a single source.

The system should consider:

* Nearby vehicles
* Obstacles
* Vehicle speed
* Relative movement
* Distance
* Visibility conditions
* Vehicle location
* Road geometry
* Other available vehicle information

This information can then be used to understand the current situation and identify potentially risky conditions.

---

## 6. Objective

The main objective of the project is to develop a safety-support system for mine vehicles that improves situational awareness during fog and low-visibility conditions.

The system aims to:

1. Detect nearby vehicles and obstacles.
2. Monitor the movement of surrounding objects.
3. Track the mine vehicle's own movement.
4. Consider visibility conditions while assessing risk.
5. Estimate the available time before a possible collision.
6. Identify potentially dangerous situations.
7. Provide timely and understandable warnings to the operator.
8. Record important safety events.
9. Identify locations where risky situations occur repeatedly.
10. Support safer and more efficient mine-vehicle operation.

---

## 7. Key Requirements

The proposed system should provide the following capabilities:

### 7.1 Nearby Object Detection

The system should identify relevant vehicles, obstacles and other objects around the mine vehicle.

### 7.2 Movement Monitoring

The system should monitor the position, speed and direction of the vehicle and nearby objects wherever the required information is available.

### 7.3 Low-Visibility Awareness

The system should take fog and reduced visibility into consideration when assessing the surrounding situation.

### 7.4 Collision-Risk Estimation

The system should estimate the possibility of a collision using information such as distance, relative speed and Time-to-Collision.

### 7.5 Timely Warning

When a potentially dangerous situation is identified, the system should provide a clear warning to the operator.

### 7.6 Near-Miss Recording

Situations where the collision risk becomes high but a collision is avoided can be recorded for further analysis.

### 7.7 High-Risk Location Identification

Repeated safety events can be analyzed to identify areas of the mine where additional attention may be required.

---

## 8. Example Problem Scenario

Consider two mine vehicles travelling on the same or intersecting mine roads during foggy conditions.

```text
             LOW VISIBILITY
                  ↓
       ┌─────────────────────┐
       │                     │
       │   VEHICLE A →       │
       │                     │
       │              ← B    │
       │                     │
       └─────────────────────┘
                  ↓
        Limited visibility
                  ↓
       Difficult to judge
       distance and movement
                  ↓
       Increased safety risk
```

The operator may not have enough visual information to understand how quickly the other vehicle is approaching.

A safety-support system can provide additional information about the detected vehicle, its distance, movement and estimated collision time.

---

## 9. Near-Miss Situation

Not every dangerous situation results in an actual collision.

For example:

```text
Vehicle A approaches Vehicle B
          ↓
Distance decreases
          ↓
TTC becomes small
          ↓
High-risk situation detected
          ↓
Operator responds
          ↓
Vehicle slows down
          ↓
Collision avoided
          ↓
Near-miss recorded
```

Recording such events can help identify repeated safety problems and locations that may require additional attention.

---

## 10. Expected Outcome

The proposed solution is expected to provide an additional layer of safety information for mine-vehicle operators.

The system aims to support:

* Better awareness of nearby vehicles
* Earlier identification of potential hazards
* Better understanding of vehicle movement
* Timely risk-based warnings
* Recording of near-miss situations
* Identification of repeated high-risk areas
* Improved decision support during low visibility

The system is intended to **support the vehicle operator**, not replace the operator's responsibility for safe vehicle operation.

---

## 11. Scope of the Problem

The project focuses specifically on the challenges faced by mine vehicles operating in:

* Open-cast iron ore mines
* Foggy conditions
* Reduced-visibility conditions
* Dusty environments
* Poor lighting conditions
* Roads with multiple vehicles
* Areas with turns and intersections

The proposed concept can be developed from a prototype into a larger mine-wide safety system after suitable testing and validation.

---

## 12. Problem-to-Solution Requirement

The problem can be summarized as:

```text
FOG / LOW VISIBILITY
          ↓
LIMITED VISUAL AWARENESS
          ↓
DIFFICULTY DETECTING VEHICLES & OBSTACLES
          ↓
DIFFICULTY JUDGING MOVEMENT & DISTANCE
          ↓
LIMITED REACTION TIME
          ↓
SAFETY RISK
```

The project addresses this by aiming to provide:

```text
MULTIPLE SOURCES OF INFORMATION
          ↓
BETTER SITUATIONAL AWARENESS
          ↓
COLLISION-RISK ESTIMATION
          ↓
TIMELY WARNING
          ↓
SAFER DECISION SUPPORT
```

---

## 13. Final Problem Definition

There is a need for a reliable safety-support system that can assist mine-vehicle operators in understanding their surroundings during fog and low-visibility conditions.

The system should use available vehicle and environmental information to detect nearby objects, understand their movement, estimate potential collision risk and provide timely warnings.

By recording safety events and analyzing repeated risky situations, the system can also support longer-term identification of high-risk areas within the mine.

The overall goal is to improve **situational awareness, safety and operational efficiency** of mine vehicles working in low-visibility conditions.


## Proposed Outcome

The project aims to support safer and more efficient operation of mine vehicles by providing additional situational information to the operator when normal visibility is reduced.
