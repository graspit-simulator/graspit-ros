# Deprecated!!!
GraspIt! now has an install target, and can be installed via 
```
git clone https://github.com/graspit-simulator/graspit.git
cd graspit
mkdir build
cd build
cmake ..
make -j5
sudo make install
```
So this repo provides no benefit as GraspIt! no longer needs to be included in each ros workspace.


# graspit-ros
ROS wrapper for the GraspIt! simulator

This repository contains wrappers and interfaces between GraspIt! and ROS. It contains a wrapper package that builds GraspIt! within the ROS framework.

## Installation

```bash
 cd ros_ws/src
 git clone https://github.com/graspit-simulator/graspit-ros --recursive
 cd ..
 catkin_make
```

## Running GraspIt!

```bash
 cd ros_ws/src/graspit-ros/graspit/graspit_source
 export GRASPIT=$PWD
 rosrun graspit graspit_simulator
```

## Exposing GraspIt! via ROS
More information can be found at http://graspit-simulator.github.io/build/html/installation_ros.html explaining how to expose GraspIt! functionality via ROS, and an example is shown here:
https://github.com/graspit-simulator/graspit_interface
