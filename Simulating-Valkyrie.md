[[images/under_construction.png]]  

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

```bash
[[images/ValInGazebo.png]]
```
