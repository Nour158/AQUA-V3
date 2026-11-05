# 🌊 AQUA V3
### Autonomous Surface Water-Cleaning Robot

**Graduation Project | College of Artificial Intelligence**

AQUA V3 is an autonomous surface-water cleaning robot designed to detect, approach and collect floating waste from marinas, lakes, canals and other suitable waterways.

The project combines **Artificial Intelligence, Computer Vision, Robotics, Embedded Systems and Autonomous Navigation** to develop a practical environmental-cleaning prototype.

> **Project status:** Early development. Mechanical prototyping and hardware evaluation are in progress. No completed robotics software or validated physical performance has been confirmed.

---

## 🎯 Project Objectives

- Detect floating trash using computer vision.
- Navigate autonomously within defined operating boundaries.
- Approach detected waste using independently controlled left and right propulsion.
- Guide floating waste toward a central conveyor using front-opening collection wings.
- Transfer collected waste into a removable storage bin.
- Monitor battery, sensors, actuators and safety conditions.
- Support manual override and emergency-stop behavior.
- Investigate a separate experimental oil-recovery mechanism.
- Log operational data for testing and evaluation.

## 🚤 Robot Design

AQUA V3 consists of:

| Component | Function |
|---|---|
| Dual hulls | Provide buoyancy and stability |
| Left/right propulsion | Control forward motion and turning |
| Front-opening wings | Guide floating waste toward the intake |
| Conveyor | Transfer waste into the bin |
| Removable waste bin | Store collected material |
| Camera | Detect floating objects |
| GNSS/GPS | Provide geographic positioning |
| IMU | Measure motion and orientation-related data |
| Main computer | Execute high-level autonomy software |
| Microcontroller | Manage low-level actuators and local safety |
| Battery | Supply electrical power |
| Solar subsystem | Potential supplemental energy source |
| Oil-recovery module | Experimental rotating-drum oil collection |

### Propulsion Status

A **12 V Johnson 750 GPH cartridge bilge-pump test unit** has been ordered for evaluation.

Its suitability for propulsion has not yet been established. Thrust, power consumption, continuous-duty suitability, reverse capability and control behavior require physical testing.

The software must support configurable propulsion adapters so that dedicated marine thrusters can replace the experimental pump approach.

## 🧠 Software Architecture

AQUA's software is planned around ROS 2.

```text
               AQUA V3 SOFTWARE
                       |
        +--------------+--------------+
        |              |              |
   PERCEPTION       AUTONOMY       MONITORING
        |              |              |
     Camera        Mission         Telemetry
     Detection     Navigation      Logging
     Tracking      Localization    Diagnostics
        |              |              |
        +--------------+--------------+
                       |
                SAFETY & CONTROL
                       |
              MCU Communication
                       |
        +--------------+--------------+
        |              |              |
    Propulsion      Collection     Oil Module
```

High-level autonomy runs on the main computer. Local actuator limits, watchdogs and critical shutdown behavior must eventually be enforced by the microcontroller.

A physical emergency-stop circuit is required independently of software stop commands.

## 📁 Repository Structure

```text
AQUA-V3/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── interface_contract.md
│   ├── mission_transitions.md
│   ├── hardware_handover.md
│   └── experiments/
├── config/
│   ├── robot.yaml
│   ├── safety.yaml
│   └── propulsion.yaml
├── ros2_ws/
│   └── src/
│       ├── aqua_interfaces/
│       ├── aqua_bringup/
│       ├── aqua_simulation/
│       ├── aqua_vision/
│       ├── aqua_autonomy/
│       ├── aqua_control/
│       ├── aqua_safety/
│       └── aqua_telemetry/
├── firmware/
│   ├── protocol/
│   └── fake_mcu/
├── datasets/
├── scenarios/
├── tests/
├── scripts/
└── .github/
    └── workflows/
```

This is the **planned structure**, not a claim that these folders and packages already exist.

## 📦 Planned ROS 2 Packages

| Package | Responsibility |
|---|---|
| `aqua_interfaces` | Custom messages, services and actions |
| `aqua_bringup` | Launch files and configuration |
| `aqua_simulation` | 2D simulation and mock hardware |
| `aqua_vision` | Detection, tracking and visual alignment |
| `aqua_autonomy` | Localization, navigation and mission logic |
| `aqua_control` | Propulsion, conveyor, wings, oil and MCU communication |
| `aqua_safety` | Watchdogs, fault handling and safety arbitration |
| `aqua_telemetry` | Monitoring, logging and replay |

## 🔄 Autonomous Mission

The proposed mission state machine includes:

```text
IDLE
  |
PREFLIGHT
  |
SEARCH
  |
APPROACH
  |
COLLECT
  |
  +---- Success ----> SEARCH
  |
  +---- Bin full ---> RETURN (if safe)
```

Additional states include:

- `SAFE_STOP`
- `MANUAL`
- `OIL_MODE`

Critical faults can interrupt autonomous operation. Return-to-home is only allowed when localization, propulsion and remaining energy are sufficient.

## 🧪 Software-First Development

Before hardware arrives, the team will develop and test:

1. ROS 2 workspace and interfaces.
2. Mock sensors and actuators.
3. Lightweight 2D simulator.
4. Mission state machine.
5. Differential propulsion controller.
6. Camera/video processing and trash detection.
7. GNSS/IMU localization adapters.
8. Waypoint navigation and geofencing.
9. Wing, conveyor and bin controllers.
10. Experimental oil-module controller.
11. MCU communication and safety watchdogs.
12. Telemetry, logging and integrated mission tests.

Simulation validates software behavior. It does not prove real-world hydrodynamics, buoyancy, thrust or waste-capture efficiency.

## 🗓️ Development Roadmap

| Phase | Proposed timeline | Focus |
|---|---|---|
| Foundation | Week 1 | Environment, repository, interfaces and mocks |
| Simulation & control | Week 2 | 2D simulation, mission, motor control and fake MCU |
| Perception & mechanisms | Week 3 | Vision, navigation, collection and telemetry |
| Integration | Week 4 | Safety, localization, oil mocks and simulated mission |
| Robustness | Weeks 5–8 | Testing, replay, documentation and integration readiness |
| Hardware integration | Following weeks | Component bring-up, calibration and physical testing |
| Final validation | Final project period | Controlled trials, evaluation and demonstration |

The overall project target is approximately **five months**. These dates are planning targets and depend on team availability and hardware progress.

## 👥 Team Responsibilities

| Member | Responsibility |
|---|---|
| P1 | Systems, interfaces, integration and documentation |
| P2 | Mechanical design and physical-test preparation |
| P3 | Electrical design, power and sensor specifications |
| P4 | MCU, propulsion, mechanism control and watchdogs |
| P5 | Computer vision, datasets, tracking and alignment |
| P6 | ROS 2, simulation, localization, navigation, mission and telemetry |

Responsibilities may be shared when workloads require it.

## 💻 Development Environment

**Proposed environment:**

- Ubuntu 24.04 LTS
- ROS 2 Jazzy
- Python 3
- Git and GitHub
- VS Code or equivalent editor

Installation instructions will be finalized after the team's operating systems, hardware resources and existing tools are verified.

The repository is not yet ready to run. Setup and build commands will be added after the environment and package skeleton are established.

## 🧰 Git Workflow

The `main` branch contains reviewed project code.

Team members should create feature branches:

```text
feature/interfaces
feature/simulation
feature/vision
feature/control
feature/navigation
feature/telemetry
```

Before merging:

1. Explain the changes.
2. Run the relevant tests.
3. Record test results.
4. Open a pull request.
5. Obtain a team review.
6. Merge only after required checks pass.

Do not commit passwords, access tokens, private credentials, large datasets or generated build files.

## 🛡️ Safety Principles

- Neutral actuator output during startup and shutdown.
- Validate all movement commands.
- Enforce command timeouts and watchdogs.
- Stop autonomous motion when localization is invalid.
- Limit actuator outputs and mechanism recovery attempts.
- Prioritize critical safety faults over mission commands.
- Provide manual override.
- Require a physical emergency-stop circuit.
- Test mechanisms individually before integrated operation.

## 📊 Testing and Verification

Software completion requires evidence, not just written code.

Testing will include:

- Unit tests
- Integration tests
- Fixed-seed simulation scenarios
- Fault-injection tests
- Recorded-data replay
- End-to-end mission demonstrations

Physical testing will later validate propulsion, sensors, mechanisms, electrical protection and collection performance.

## 📌 Current Project Status

| Item | Status |
|---|---|
| AQUA V3 concept | Defined |
| Demonstration model | Printing in progress |
| Hull-material selection | Advice pending |
| Johnson pump | Ordered for testing |
| Propulsion performance | Not verified |
| ROS 2 environment | Not confirmed |
| Software repository contents | Being established |
| Simulator | Not implemented |
| Vision model | Not implemented |
| Hardware integration | Pending |

## 🔗 Project Management

**AQUA V3 Buildboard**

https://aqua-v3-buildboard.admirableactor.chatgpt.site

This board is intended for project-management checklists and progress tracking. It is separate from the robot's operational telemetry interface.

---

**AQUA V3 — Building an intelligent robot for cleaner waterways.**

*Developed as an Artificial Intelligence graduation project.*
