### Assumptions

This guide assumes you have Ubuntu 14.04 installed. 

***

### Setup Apt Sources

We pull Debians from ROS and Gazebo, as well as our own apt server. You'll need to add these to your /etc/apt/sources.list.d/ directory.
Run the following lines:

    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116
 
    sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-latest.list'
    sudo wget -O - http://packages.osrfoundation.org/gazebo.key | sudo apt-key add -

Update your apt sources.  

    sudo apt-get update

Optional, but recommended.  

    sudo apt-get upgrade

***

### Setup Users and Groups

Configure your users and groups with the following:

    sudo groupadd ros
    sudo usermod -aG ros $USER
    sudo adduser vanguard
    sudo usermod -aG sudo vanguard
    sudo usermod -aG ros vanguard

***

### Install Developer Dependencies

This step will install ros-indigo, support packages for Orocos, and standard developer tools/libraries.  

Install Common Base Packages:

    sudo apt-get install wget curl apt-utils nano vim htop python-pip python-vcstool python-rosdep python-rosinstall python-dev libzmq1 libzmq-dev libprotobuf-dev google-mock lm-sensors openssh-server build-essential git-flow protobuf-compiler ros-indigo-catkin syslog-ng syslog-ng-core

**Please choose ONE** of the two options below. ROS Headless will install ros-indigo-ros-base. ROS Desktop will install ros-indigo-desktop-full.

Install ROS Headless:  

    sudo apt-get install ros-indigo-ros-base ros-indigo-rtt-ros ros-indigo-orocos-toolchain ros-indigo-rtt-ros-integration ros-indigo-rtt-geometry ros-indigo-rtt-common-msgs ros-indigo-rtt-ros-comm ros-indigo-xacro ros-indigo-ros-control ros-indigo-ros-controllers

Install ROS Desktop:  

    sudo apt-get install ros-indigo-desktop-full ros-indigo-rtt-ros ros-indigo-orocos-toolchain ros-indigo-rtt-ros-integration ros-indigo-rtt-geometry ros-indigo-rtt-common-msgs ros-indigo-rtt-ros-comm ros-indigo-xacro ros-indigo-ros-control ros-indigo-ros-controllers

***

### Install NASA Debians

Download the following Debians:
[nasa-indigo-workspace](https://drive.google.com/file/d/0B4Esozi1aH0sZFJPSTVFNy1OM1k/view?usp=sharing)
[nasa-val-system-config](https://drive.google.com/file/d/0B4Esozi1aH0sMk15TThrVlZYRVk/view?usp=sharing)

Install those Debians with the following commands:

    sudo dpkg -i nasa-indigo-workspace nasa-val-system-config

***

### Setup Rosdep

Init rosdep.

    sudo rosdep init

Add sources to your rosdep lists.

    sudo sh -c 'echo "yaml https://raw.githubusercontent.com/NASA-JSC-Robotics/nasa_common_rosdep/master/nasa-common.yaml"  > /etc/ros/rosdep/sources.list.d/30-nasa-common.list'
    sudo sh -c 'echo "yaml https://raw.githubusercontent.com/NASA-JSC-Robotics/nasa_common_rosdep/master/nasa-trusty.yaml"  > /etc/ros/rosdep/sources.list.d/31-nasa-trusty.list'
    sudo sh -c 'echo "yaml https://raw.githubusercontent.com/NASA-JSC-Robotics/nasa_common_rosdep/master/nasa-gazebo4.yaml" > /etc/ros/rosdep/sources.list.d/32-nasa-gazebo4.list'

Update your sources. DO NOT run as root.

    rosdep update

***

### Setup Environment

Run the following:

    python /usr/local/share/nasa/setup_nasa_val_user_bash.py

Add the following to the bottom of your ~/.bashrc file:

    if [ -f ~/.bash_nasa_val ]; then
        source ~/.bash_nasa_val
    fi

Finally, source your ~/.bashrc file:

    source ~/.bashrc