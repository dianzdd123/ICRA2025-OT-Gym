# Reusing ICRA2025-OT-Gym

Optical-tweezer microrobotics simulation and haptic control.

**Current scope:** Archive-based research release: source, models and scenes are distributed in ZIP files.

This repository is a fork of [Zongcai23/ICRA2025-OT-Gym](https://github.com/Zongcai23/ICRA2025-OT-Gym). Original authorship, citations and upstream notices are retained. Changes here apply to this fork.

## What is actually included

| Archive | Contents |
|---|---|
| `RL_navigation_code.zip` | DQN scripts, deployment script, `best_model_750.pth` and `smoothed_path.csv` |
| `Bimanual_haptic_feedback_control_code.zip` | Left/right ROS 1 catkin workspaces, including historical build outputs |
| `3DModel.zip` | USD robot/model assets |
| `SimEnv_R0820V2forRLexperiment.zip` | RL experiment scene |
| `SimEnv_R0821forSharedControlExperiment.zip` | Shared-control scene |
| `SimEnv_R0823forHumanControlwithoutDynamic.zip` | Manual-control scene |
| `SimEnv_R0918forSharedControlExperiment.zip` | Additional shared-control scene |
| `Visualization_rendering_video.zip` | Rendering and experiment videos |

## Inspect before running

```bash
python scripts/check_repository.py
python -m zipfile -l RL_navigation_code.zip
python -m zipfile -t RL_navigation_code.zip
```

The first command checks the unpacked repository only. ZIP listing and integrity checks do not execute the archived scripts or verify simulator compatibility. Extract the selected archives into a separate local working directory, preserving the original release files.

## Reconstruct the experiment environment

The original README identifies Linux, Python 3.10, Isaac Sim 4.1.0 and ROS 1. Do not substitute a different simulator version without checking the ROS bridge and scene APIs. Bimanual teleoperation additionally needs two Geomagic Touch devices and their drivers.

After extracting the haptic archive, rebuild each catkin workspace for your machine from its `src/` tree. Packaged `build/` and `devel/` files contain machine-specific paths. Source your installed ROS environment before compiling; source the newly generated `devel/setup.bash` afterwards. Configure device permissions using your platform's driver/udev setup.

Update USD asset references, robot/scene paths and host addresses before opening the simulation. Inspect the extracted launch files to select the actual package and launch names. There is no root `launchIsaacSim.sh` or installed `rl_navigation` ROS package in this Git checkout; use the matching simulator launcher and extracted Python scripts.

## Expected outputs and reproduction record

The navigation workflow consumes a scene, network weights and path data; teleoperation consumes device/ROS inputs. Capture trajectories, success criteria and task settings separately from videos. Record archive hashes, simulator/ROS versions, checkpoint identity, scene changes and device calibration. Hardware-in-the-loop and learning results have not been reproduced by the structural checks.

## Attribution and reuse permissions

No repository-wide licence file is included in this checkout. Confirm reuse and redistribution permissions with the relevant rights holders; this maintenance update does not add a licence or relicense upstream code, data or assets.

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the local workflow and what to include with a proposed change.
