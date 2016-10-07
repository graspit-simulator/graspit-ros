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
 rosrun graspit graspit_simulator
```

## Exposing GraspIt! via ROS
More information can be found at http://graspit-simulator.github.io/build/html/installation_ros.html explaining how to expose GraspIt! functionality via ROS.
