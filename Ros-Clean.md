Use this script to nuke your ROS environment and start over. 

When rebuilding start from the top down. Source /opt/ros/indigo, then /opt/nasa/indigo, then the val_indigo, then third party, then any other.

```bash
#!/bin/bash
 
export CMAKE_PREFIX_PATH=
export CPATH=
export ROS_ROOT=
export ROS_DISTRO=
export ROS_WORKSPACE=
export ROS_PACKAGE_PATH=
export ROS_ETC_DIR=
export PKG_CONFIG_PATH=
export PYTHONPATH=
export ROSLISP_PACKAGE_DIRECTORIES=
export LUA_PATH=
export LUA_CPATH=
export GAZEBO_MODEL_PATH=
export GAZEBO_RESOURCE_PATH=
export LD_LIBRARY_PATH=
export ROS_TEST_RESULTS_DIR=
export RTT_COMPONENT_PATH=
```