# 📝 Interactive OT Gym: A Reinforcement Learning-Based Interactive Optical tweezer (OT)-Driven Microrobotics Simulation Platform

## Start here

This repository is a fork of [Zongcai23/ICRA2025-OT-Gym](https://github.com/Zongcai23/ICRA2025-OT-Gym). Original authorship, citations and upstream notices are retained. Changes here apply to this fork.

**Scope:** Archive-based research release: source, models and scenes are distributed in ZIP files.

| Need | Where to start |
|---|---|
| Setup, file map, inputs/outputs and troubleshooting | [Reuse guide](docs/REUSE.md) |
| Local structural validation | `python scripts/check_repository.py` (Python 3.10+) |
| Proposed fixes and reproducibility details | [Contributing](CONTRIBUTING.md) |

The structural check does not run experiments or certify hardware, model accuracy or dependency compatibility. Reuse permissions need clarification: this checkout has no repository-wide licence file.


## ✍️ Authors & Affiliations  
**Zongcai Tan**, Imperial College London  
**Dandan Zhang**, Imperial College London  

## 🔗 Project Links  
[Website](https://sites.google.com/view/otgym) | [Short Video](https://drive.google.com/file/d/1qvTl7QsJqCCDp0TmPr03gavFDYRkFXab/view?usp=sharing) | [Long Video](https://drive.google.com/file/d/1IxezuWqVQzHAi8P1-euABZsLCVHTun7e/view?usp=sharing)

## 🛠️ Status & Requirements  
![IsaacSim 4.1.0](https://img.shields.io/badge/IsaacSim-4.1.0-lightgrey) ![Python 3.10](https://img.shields.io/badge/Python-3.10-blue) ![Platform Linux-64](https://img.shields.io/badge/Platform-Linux--64-brightgreen)


## 📖 Overview  
![Overview Diagram](overview.jpg)  
OT-Gym is a physics-based optical micro-robot simulation framework built on NVIDIA Isaac Sim to train reinforcement-learning algorithms for micro-manipulation tasks. This repo provides code and simulation environments for:  
- **Bimanual haptic-feedback control**  
- **RL-based autonomous control**  
- **Shared-control navigation for cell sorting**  
using optical-tweezer-actuated microrobots.  

## ✨ Features  

### 🤖 Shared OT Micromanipulation Process  
![Shared OT Micromanipulation GIF](shared_ot_process.gif)  
Users first indirectly grasp target cells using optical robots, then transport the cells to designated locations before releasing them.  

### 📈 Effectiveness Validation Experiment  
![Shared Control Validation GIF](shared_control_validation.gif)  
Manual control is safe yet inefficient, autonomous control is efficient but collision-prone, and shared control balances efficiency with safety.  

## 📋 Requirements  

### 🖥️ Hardware  
- Two **Geomagic Touch** haptic devices for teleoperation  
- Two computers with **ROS 1** (ROS 2 _not_ supported)  
- One “main” computer with NVIDIA Isaac Sim installed  

### 💾 Software  
- **ROS 1** on both machines  
- **Isaac Sim 4.1.0** (original release target; verify bridge compatibility) on the main machine
- Extraction paths must contain only ASCII characters  
- All devices on the same LAN  

## 📚 User Guide  

### 1. Basic Setup  
OT-Gym builds on NVIDIA Isaac Sim. See the [Isaac Sim docs](https://developer.nvidia.com/isaac/sim). 

### 2. Bimanual Haptic-Feedback Teleoperation 
Download the Bimanual_haptic_feedback_control_code.zip package. Deploy the Left_hand_geomagic_touch_control and Right_hand_geomagic_touch_control workspaces on the two computers configured with Geomagic Touch devices. Compile the code and complete the basic setup.
```bash
# Download & unzip
unzip Bimanual_haptic_feedback_control_code.zip

# Configuring the device
./Touch_Setup
# Configure the actual device using the driver/udev instructions.

# Compile the code
# Machine 1 (Left hand)
cd Left_hand_geomagic_touch_control
source ./devel/setup.bash
catkin_make
# Machine 2 (Right hand)
cd Right_hand_geomagic_touch_control
source ./devel/setup.bash
catkin_make

# On each machine
roscore                # if not already running
roslaunch geomagic_control geomagic.launch
```

### 3. RL Navigation Setup  
```bash
# Download & unzip RL navigation
unzip RL_navigation_code.zip

# Ensure ASCII-only paths
# Place RL code alongside Isaac Sim examples
mv RL_navigation_code path/to/IsaacSim/examples/

# Update paths in code if needed:
# - DQN_env.py → Drives the robot for shared control.
# - deploy_best_model.py → Drives the robot for full autonomous control (RL).
# - best_model_750.pth → RL-trained network parameters
# - smoothed_path.csv → Stores the optimal path calculated by the A* algorithm.
```

### 4. Simulation Environment  
```bash
# Download & unzip Sim environment & 3D models
for archive in SimEnv_*.zip; do unzip "$archive"; done
unzip 3DModel.zip

# On main computer:
roscore

# Open the extracted USD scene using the configured ROS1 bridge.
# Update all referenced USD paths for your local checkout.
```  
- Load USD files via the ROS1 bridge in Omniverse  
- Update USD file paths to avoid errors  

### 5. Running the demo

Use the launch files present in the extracted ROS workspaces and the launcher supplied by your matching Isaac Sim installation. The root checkout does not include `launchIsaacSim.sh` or an installed `rl_navigation` ROS package. Inspect the extracted `deploy_best_model.py`, set its local scene/checkpoint paths, and run it with the simulator's Python environment after configuring the ROS 1 bridge.

## Release contents

See the [archive inventory and setup guide](docs/REUSE.md) for the exact ZIP filenames, prerequisites, rebuilding guidance and validation limits. The root images `overview.jpg`, `shared_ot_process.gif` and `shared_control_validation.gif` illustrate the project; datasets and models are described separately in the archive inventory.
