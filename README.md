# Sunroof Control Module Capstone

A CANoe-based simulation of an automotive sunroof control module (SCM), implemented with CAPL and a shared CAN database. The project models user commands, sunroof position and motor status, obstruction handling, and automated test scenarios.

## Project contents

| File | Purpose |
| --- | --- |
| `SunroofControlModule_Clean.can` | CAPL logic for the sunroof controller and its state transitions. |
| `Panel_Sim_Clean.can` | CAPL logic for the panel simulation and command generation. |
| `SunroofControlModule_Clean.dbc` | CAN database defining command (`0x201`) and status (`0x200`) messages. |
| `Sunroof_Automated_Test_Clean.can` | Automated CANoe test module for command and status behavior. |
| `Sunroof_Automated_Test.tse`, `Sunroof_Automated_Test.sttse` | CANoe test environment and sequence configuration. |
| `Panel1.xvp` | CANoe panel layout. |
| `*.cbf` | CANoe configuration/binary assets included with the project. |

The capstone report is intentionally not included in this repository.

## Features modeled

- Open, close, tilt, and one-touch-close commands
- Sunroof position reporting (0% fully open to 100% fully closed)
- Motor current reporting
- Pinch/obstruction detection and stop behavior
- Timeout abort reporting for one-touch close
- Automated test sequence support

## CAN interface

The DBC defines these frames:

| Message | CAN ID | Direction | Signals |
| --- | ---: | --- | --- |
| `SCM_Command` | `0x201` | Panel → SCM | `OpenBtn`, `CloseBtn`, `TiltBtn`, `OneTouchCmd` |
| `SCM_Status` | `0x200` | SCM → Panel | `SunroofPosition`, `MotorCurrent`, `PinchDetected`, `AbortTimeout` |

## Running in Vector CANoe

1. Use a Windows environment with a compatible Vector CANoe installation and licenses.
2. Open the supplied CANoe configuration/project assets (`.cbf` and `.xvp`) in CANoe.
3. Confirm that both CAPL nodes use `SunroofControlModule_Clean.dbc` and that their CAN channels are connected in the simulation setup.
4. Start the measurement and operate the panel controls to send commands.
5. Open the included test environment/sequence (`Sunroof_Automated_Test.tse` / `.sttse`) in the CANoe Test Feature Set and run the automated tests.
6. Inspect CANoe trace, panel indicators, position, current, pinch, and timeout status during the simulation.

Exact CANoe menu steps and compatibility depend on the installed CANoe version and project configuration. This project is a simulation artifact; it is not validated for use in a production vehicle.

## Requirements

- Windows
- Vector CANoe with CAPL and the CANoe Test Feature Set (for automated tests)

No Python packages are required.

## License

No license file was supplied with the source bundle. Add a license before redistributing or reusing this project.
