# Prerequisites
To follow these instructions, you must first have the following:
* Valkyrie Software(get that [here](https://github.com/NASA-JSC-Robotics/valkyrie/wiki/Get-Valkyrie-Code))
* Gazebo 4(Instructions for upgrading from Gazebo 2.x to Gazebo 4.x can be found [here](http://gazebosim.org/tutorials/?tut=ros_wrapper_versions))

## Start Simulating
Once you have all of the Valkyrie software on your computer, make sure it's compiled and installed,

```bash
cd ~/val_indigo && catkin_make install
```

Now you need to launch the sim. Currently the Valkyrie software comes with a pinned sim in which Valkyrie is pinned at the torso as well as a full simulator where the robot is not pinned. To launch the pinned simulator, simply execute in a terminal,

```bash
roslaunch val_gazebo val_sim_pinned.launch
```

or for the full unpinned sim, run the following command,

```bash
roslaunch val_gazebo val_sim.launch
```

In either case the Gazebo simulator will come up showing Valkyrie,

[[images/ValInGazebo.png]]

These launch scripts also launch a [controller manager](http://wiki.ros.org/controller_manager), so the controller manager is sitting and waiting to load ROS controllers. For info on how to write ROS controllers, we have a page with some rough instructions [here](How To Write A Controller For Valkyrie) or you can refer to the [ROS control wiki](http://wiki.ros.org/ros_control).

Additionally, if you are interested in using [IHMC](http://robots.ihmc.us/)'s controller you may visit the [IHMC wiki](http://ihmcrobotics.github.io/). You can find their Valkyrie specific ROS control stuff [here](https://github.com/ihmcrobotics/ihmc_valkyrie_ros).