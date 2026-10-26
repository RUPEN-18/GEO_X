# GeoX — 6-DOF Mobile Manipulator Rover

**Third-year robotics project by Rupendran Manigandan**

GeoX is a mobile manipulator: a rover that combines a wheeled base with a **six-degree-of-freedom robotic arm**. The base provides mobility, while the arm provides object interaction and manipulation. The project brings together rover movement, robotic actuation, and LiDAR-oriented environmental sensing in a Raspberry Pi-based platform.

**The 6-DOF designation refers to the robotic arm.**

This repository contains **a partial collection of the project's available Python code**. It documents the hardware project and preserves the available movement, arm-control, and sensing examples. It does not contain the complete original software or a ready-to-run autonomous navigation system.

## Project at a glance

| Item | Description |
| --- | --- |
| Project name | GeoX |
| Academic stage | Third-year engineering project |
| Robot type | Mobile manipulator: wheeled rover with a robotic arm |
| Arm configuration | 6-DOF, as identified by the project author |
| Computing platform | Raspberry Pi, as described in the original project documentation |
| Main language in this repository | Python |
| Repository scope | Partial source code and project documentation |

## Hardware project and available software

GeoX's project scope includes a mobile base, a 6-DOF arm, and LiDAR-based environmental sensing. The available files represent individual control examples and a demonstration integration loop.

| Area | What the available code actually contains |
| --- | --- |
| Rover movement | GPIO commands for forward movement, stopping, and left/right turns |
| Arm control | An example servo sequence using Adafruit ServoKit |
| Distance sensing | A simulated distance provider returning random values |
| Integration logic | A distance-threshold demonstration combining movement and an example arm action |
| Navigation and mapping | No real LiDAR driver, SLAM, localization, or path-planning implementation is present |
| Vision | OpenCV is listed as a dependency, but no vision processing is implemented in the available files |

The repository's simulated LiDAR module should not be used as real obstacle feedback for operating the rover.

## Available files

| File | Purpose |
| --- | --- |
| [main.py](main.py) | Demonstration loop that reads a distance, chooses movement, and triggers a sample arm action |
| [rover_movement.py](rover_movement.py) | Raspberry Pi GPIO-based rover movement class |
| [Rover_arm control.py](Rover_arm%20control.py) | Example arm sequence using selected servo channels |
| [rover_lidar.py](rover_lidar.py) | Placeholder LiDAR class that generates simulated distance values |
| [Requirements.txt](Requirements.txt) | Existing dependency list |

The source filenames are preserved as uploaded.

## How the available examples work

### Rover movement

`RoverMovement` configures four GPIO outputs using **BCM numbering: 17, 18, 22, and 23**. Its methods set those outputs for forward movement, stopping, and left/right turns.

These values describe the code's pin selections. They do not establish the complete motor-driver wiring, power design, or original chassis configuration.

### Robotic arm

`RoboticArm` creates a 16-channel `ServoKit` interface. The `pick_object()` example commands servo channels **0, 1, 2, and 5** with fixed angles and delays.

This is a sample actuation sequence. The available code does not include complete six-joint control, inverse kinematics, joint calibration, motion planning, or feedback confirming that an object was grasped. Its printed “Object picked” message is not a success measurement.

### Sensing and demonstration loop

`LiDAR.get_distance()` currently returns a random integer from **10 to 100**. It does not communicate with a physical LiDAR sensor.

The demonstration in `main.py` treats distances below **30 cm** as an obstacle condition and distances below **15 cm** as a trigger for the example arm action. These are demonstration thresholds applied to simulated input, not evidence of a validated autonomous navigation system.

## Current integration status

The repository is **not runnable as a complete application in its current layout**:

- `main.py` imports `rover.movement`, `rover.lidar`, and `rover.arm_control`, but the corresponding `rover/` package is absent.
- The available movement, arm, and sensing files are stored at the repository root under different names.
- The real LiDAR interface and the complete original project software are not available here.
- Hardware-specific configuration, wiring, servo limits, and calibration are not fully documented.

These limitations describe this collection of files; they do not establish which functions were demonstrated on the original physical project.

## Dependencies

The existing [Requirements.txt](Requirements.txt) lists:

- `RPi.GPIO` — used by the movement example.
- `adafruit-circuitpython-servokit` — used by the arm example.
- `numpy`, `opencv-python`, and `pyserial` — listed in the original dependency file, but not imported by the available source files.

Hardware-dependent examples require a compatible Raspberry Pi environment and the appropriate connected hardware. Installing these dependencies alone does not resolve the missing package layout or supply a real LiDAR driver.

## Continuing the project

1. Recover and document any additional original firmware, control scripts, wiring diagrams, and hardware details.
2. Organize the available modules into the package structure expected by `main.py`, or update the imports in a separate code revision.
3. Restore the real LiDAR interface and keep simulated sensing explicitly separate from hardware operation.
4. Document the arm's joint/channel mapping, calibrated limits, motor driver, and power arrangement.
5. Validate each subsystem before testing the integrated rover.

## Verification

This documentation was checked against the six files present in the repository on **26 October 2026**. The source code has not been modified as part of this documentation update. No hardware execution, navigation evaluation, or arm calibration was performed.

## Author

**Rupendran Manigandan**  
GeoX — third-year 6-DOF mobile manipulator rover project.
