### Assumptions

This guide assumes you have Ubuntu 14.04 installed. 

***

### Setup Apt Sources

We pull Debians from ROS and Gazebo, as well as our own apt server. You'll need to add these to your /etc/apt/sources.list.d/ directory.
Run the following lines:

    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116
 
    sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
    sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-keys D2486D2DD83DB69272AFE98867170598AF249743

Update your apt sources.  

    sudo apt-get update

Optional, but recommended.  

    sudo apt-get upgrade

***

### Setup Users and Groups

Configure your users and groups with the following:


    sudo groupadd ros
    sudo groupadd pgrimaging
    sudo adduser vanguard
    sudo usermod -a -G ros $USER
    sudo usermod -a -G dialout $USER
    sudo usermod -a -G pgrimaging $USER
    sudo usermod -a -G sudo vanguard
    sudo usermod -a -G ros vanguard

***

### Install Developer Dependencies

This step will install ros-indigo, support packages for Orocos, and standard developer tools/libraries.  

Install Common Base Packages:

    sudo apt-get install wget curl apt-utils nano vim htop python-apt python-pip python-vcstool python-rosdep python-rosinstall python-dev libzmq1 libzmq-dev libprotobuf-dev google-mock lm-sensors openssh-server build-essential git-flow protobuf-compiler ros-indigo-catkin syslog-ng syslog-ng-core dkms liblzo2-dev

**Please choose ONE** of the two options below. ROS Headless will install ros-indigo-ros-base. ROS Desktop will install ros-indigo-desktop-full.

Install ROS Headless:  

    sudo apt-get install ros-indigo-ros-base ros-indigo-rtt-ros ros-indigo-orocos-toolchain ros-indigo-rtt-ros-integration ros-indigo-rtt-geometry ros-indigo-rtt-common-msgs ros-indigo-rtt-ros-comm ros-indigo-xacro ros-indigo-ros-control ros-indigo-ros-controllers

Install ROS Desktop:  

    sudo apt-get install ros-indigo-desktop-full ros-indigo-rtt-ros ros-indigo-orocos-toolchain ros-indigo-rtt-ros-integration ros-indigo-rtt-geometry ros-indigo-rtt-common-msgs ros-indigo-rtt-ros-comm ros-indigo-xacro ros-indigo-ros-control ros-indigo-ros-controllers

***

### Install NASA Debians

Download the following Debians:  
[nasa-indigo-workspace](https://drive.google.com/file/d/0B4Esozi1aH0sZFJPSTVFNy1OM1k/view?usp=sharing)  
[nasa-val-system-config](https://drive.google.com/file/d/0B4Esozi1aH0sbllHUTFvN0dnOXc/view?usp=sharing)  

Install those Debians with the following commands:

    sudo dpkg -i nasa-indigo-workspace*.deb nasa-val-system-config*.deb

***

### Setup Rosdep

Init rosdep.

    sudo rosdep init

Add sources to your rosdep lists.

    sudo sh -c 'echo "yaml https://raw.githubusercontent.com/NASA-JSC-Robotics/nasa_common_rosdep/master/nasa-common.yaml"  > /etc/ros/rosdep/sources.list.d/10-nasa-common.list'
    sudo sh -c 'echo "yaml https://raw.githubusercontent.com/NASA-JSC-Robotics/nasa_common_rosdep/master/nasa-trusty.yaml"  > /etc/ros/rosdep/sources.list.d/11-nasa-trusty.list'
    sudo sh -c 'echo "yaml https://raw.githubusercontent.com/NASA-JSC-Robotics/nasa_common_rosdep/master/nasa-gazebo4.yaml" > /etc/ros/rosdep/sources.list.d/12-nasa-gazebo4.list'

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

***

Please proceed to the second part:
[Checking out Valkyrie source code](Valkyrie-Source-Code)