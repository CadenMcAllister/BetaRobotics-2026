# LEGO SPIKE Prime Beta Robotics Project

## Overview
This repository serves as documentation and backup for my team's Beta Club Robotics competition project. The system implements autonomous movement control for LEGO SPIKE Prime robots using gyroscopic stabilization and dual control methodologies.

## Movement Control Systems

### Distance-Based Movement System
The distance-based system uses wheel encoder feedback for precise positional control:

- **Unit Conversion**: Converts inch inputs to centimeters using the [original video's formula](https://www.youtube.com/watch?v=AW5yaJMTzEw&t=256s) as reference
- **Distance Calculation**: Determines required wheel rotations based on 17.5 cm wheel circumference
- **Degree Conversion**: Translates wheel rotations into target degrees for motor encoder tracking
- **Position Monitoring**: Tracks `RelativePosition` (cumulative wheel degrees) against calculated targets
- **Loop Control**: Executes `repeat until relative position < RelativePosition` for precise stopping
- **Applications**: Critical for scoring zones, waypoint navigation, and measured field traversal

### Time-Based Movement System  
The time-based system provides duration-controlled movement for simplified autonomous routines:

- **Timer Control**: Utilizes `wait 0.5 seconds` for processing delays and timer resets
- **Streamlined Operation**: Eliminates complex encoder calculations in favor of consistent timing
- **Fixed Duration**: Executes movement for predetermined time intervals
- **Use Cases**: Rapid deployment sequences, time-critical maneuvers, and backup navigation strategies

## Gyroscopic Stabilization Algorithm
Both systems implement identical correction logic for straight-line stability:

1. **Heading Error**: Calculates `Correction = Heading - yaw_angle` to determine drift
2. **Angular Compensation**: Handles 360° wraparound by adding 360° when correction < -180°
3. **Differential Control**: Applies `Left motor = MoveSpeed + Correction` and `Right motor = MoveSpeed - Correction`
4. **Continuous Adjustment**: Maintains course correction throughout movement execution

## System Comparison
| Feature | Distance-Based | Time-Based |
|---------|----------------|------------|
| **Termination** | Encoder position | Fixed duration |
| **Precision** | High accuracy | Approximate |
| **Complexity** | Advanced calculations | Simple implementation |
| **Best Use** | Scoring, navigation | Quick maneuvers, backup routines |

## Forklift Control System
The forklift mechanism enables vertical manipulation of game pieces through precise motor control:

- **Lift Functions**: Implements `Descend` and `Elevate` functions for controlled vertical movement
- **Rotation Conversion**: Motor rotations are converted using a 1.3 ratio factor because one full motor rotation does not equal one full lift cycle
- **Dual Direction Control**: 
  - `Descend`: Runs motor D in reverse direction for lowering operations
  - `Elevate`: Runs motor D in forward direction for raising operations
- **Precision Control**: Uses `DLiftValue` and `ELiftValue` variables with rotation-based positioning
