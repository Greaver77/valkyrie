## The Valkyrie Environment  
The Valkyrie environment configuration is comprised of a decent number of moving parts. The goal of this page is to layout our configurations and expose those moving parts so that they are easier to understand.  

OS: Ubuntu 14.04.2 LTS  
ROS Version: ROS Indigo LTS  
Gazebo Version: Gazebo 4  

##### But first, a note about ROS  
Our configuration is heavily dependent on ROS. ROS handles the bulk of its configuration with environment variables and catkin workspaces. For more information about ROS please see: http://wiki.ros.org/ROS/EnvironmentVariables  

##### Back to our regularly scheduled program  
The four major parts of our environment path are as follows.  

<PICTURE HERE>

    /opt/ros/indigo - The location of the workspace for installed ROS (Indigo) Debian packages.
    /opt/nasa/indigo - The location of the workspace for installed NASA ROS (Indigo) Debian packages.
    /home/<user>/val_indigo - The location of the workspace for Valkyire source code.
    /home/<user>/controller_ws - The location of the workspace for third-party source code.

These four parts are sourced left to right in the diagram above. The red blocks are paths that must exist on the system. The blue blocks are optional locations that will be included if they exist. The diagram above results in a     ROS_PACKAGE_PATH that is configured like the example below.

    ROS_PACKAGE_PATH=/home/<USER>/val_indigo/install/share:/home/<USER>/val_indigo/install/stacks:/opt/nasa/indigo/share:/opt/nasa/indigo/stacks:/opt/ros/indigo/share:/opt/ros/indigo/stacks

When searching for a requested item in the ROS_PACKAGE_PATH, the path is traversed left to right. This allows for our system to have installed Debians and source code to checked out simultaneously (with source code overriding installed Debians). While we expect the bulk of our codebase to be run from Debians, the val_Indigo workspace grants us the flexibility to checkout source code for feature or bug testing.

## Valkyrie Environment Debian Packages
Their are two primary packages needed to setup the Valkyrie environment.

* nasa-indigo-workspace

This package adds a workspace specific to NASA generated Debians at /opt/nasa/indigo. This is similar to the ROS workspace for installed Debians located at /opt/ros/<rosversion>.
This package ensures that our other Debians have a consistent location to install too. This location is then added and sourced by our setup scripts. 

* nasa-val-system-config

This package comes in a number of flavors with additional suffixes, but nasa-val-system-config is the most generic. nasa-val-system-config installs a set of configuration files to prep the system for development of Valkyrie code. Additional scripts provided by nasa-val-system-config allow users to further setup their development environment variables. After running these scripts, a users .bashrc file will automatically source things in the correct order. 
While it is our goal to eventually have a generic robot discovery system, our current setup requires that the robot and the visualizer workstation have matched nasa-val-system-configuration packages. The following list contains all current configurations.  

    common, link01, link02, link03, link04, vis01, vis02, vis03, vis04, zelda01, zelda02, zelda03, zelda04

## Environment Files
The table listed below walks you through, in order, what files live where, what order they are sourced in, and any environment variables set.  

Header | Other Header | other other header
:--------:|--------:|:--------|--------
centered | right aligned | left aligned | Regular
Cell Stuff 1b | *Cell* Stuff 2b | stuff | align


Step | Filepath | Notes | Variables Set
:--------:|:--------|:--------|:--------
1 | ~/.bashrc | Sources ~/.bash_nasa_val | 
2 | ~/.bash_nasa_val | Sources contents of ~/.bash_nasa_val.d |
3 | ~/.bash_nasa_val.d/00_bash_nasa_val_config | Sets generic variables and generic system configurations |
4 | ~/.bash_nasa_val.d/01_bash_ros - Part 1 | Sources /etc/nasa-val |
5 | /etc/nasa-val | Sources contents of /etc/nasa-val.d |
6 | /etc/nasa-val.d/ros_env.sh - Part 1	| Sets ROS_DISTRO. Sources /opt/ros/indigo/setup.bash | ROS_DISTRO=indigo |
7 | /opt/ros/indigo/setup.bash | Prepends ROS_PACKAGE_PATH | ROS_PACKAGE_PATH=/opt/ros/indigo/share:/opt/ros/indigo/stacks |
8 | /etc/nasa-val.d/ros_env.sh - Part 2 | Sources /opt/nasa/indigo/setup.bash |
9 | /opt/nasa/indigo/setup.bash | Prepends ROS_PACKAGE_PATH | ROS_PACKAGE_PATH=/opt/nasa/indigo/share:/opt/nasa/indigo/stacks:$ROS_PACKAGE_PATH |
10 | /etc/nasa-val.d/ros_net.sh	| Sets ROS_MASTER_URI. Sets ROS_IP. This file does not exist in the generic nasa-val-system-config Debian package | ROS_MASTER_URI=http://<Link processor ip here>:11311 ROS_IP=<current machines ip here> |
11 | ~/.bash_nasa_val.d/01_bash_ros - Part 2 | Sets VAL_WORKSPACE. Sets workspace hierarchy for val_indigo and prepends ROS_PACKAGE_PATH | VAL_WORKSPACE=~/val_indigo ROS_PACKAGE_PATH=/home/<user>/val_indigo/install/share:/home/<user>/val_indigo/install/stacks:$ROS_PACKAGE_PATH |
12 | ~/.bash_nasa_val.d/02_controller | Sets CONTROLLER_WORKSPACE. Sets workspace hierarchy for controller_ws and prepends ROS_PACKAGE_PATH | CONTROLLER_WORKSPACE=~/controller_ws ROS_PACKAGE_PATH=/home/<user>/controller_ws/install/share:/home/<user>/controller_ws/install/stacks:$ROS_PACKAGE_PATH |
13 | ~/.bash_nasa_val.d/10_bash_nasa_val_aliases | Sets helpful alias values |
