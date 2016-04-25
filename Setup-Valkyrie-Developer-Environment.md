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

This step will install the core dependencies, support packages, and standard developer tools/libraries required by the Valkyrie development environment.  

Install the following packages:

    sudo apt-get install binutils ca-certificates cpp cpp-4.8 curl fontconfig fontconfig-config fonts-dejavu-core g++ g++-4.8 gcc gcc-4.8 git git-flow htop iso-codes krb5-locales libamd2.3.1 libasan0 libatomic1 libaudio2 libavahi-client3 libavahi-common-data libavahi-common3 libblas3 libc-dev-bin libc6-dev libcamd2.3.1 libccolamd2.8.0 libcholmod2.1.2 libcloog-isl4 libcolamd2.8.0 libcups2 libdrm-intel1 libdrm-nouveau2 libdrm-radeon1 libelf1 libexpat1-dev libfontconfig1 libfreetype6 libgcc-4.8-dev libgfortran3 libgl1-mesa-dri libgl1-mesa-glx libglapi-mesa libglib2.0-0 libglib2.0-data libgmp10 libgomp1 libgssapi-krb5-2 libgstreamer-plugins-base1.0-0 libgstreamer1.0-0 libice6 libisl10 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 liblapack3 liblcms2-2 libllvm3.4 libmpc3 libmpfr4 libmysqlclient18 liborc-0.4-0 libpciaccess0 libpython-dev libpython-stdlib libpython2.7 libpython2.7-dev libpython2.7-minimal libpython2.7-stdlib libqt4-dbus libqt4-declarative libqt4-designer libqt4-help libqt4-network libqt4-opengl libqt4-script libqt4-scripttools libqt4-sql libqt4-sql-mysql libqt4-svg libqt4-test libqt4-xml libqt4-xmlpatterns libqtassistantclient4 libqtcore4 libqtdbus4 libqtgui4 libqtwebkit4 libquadmath0 libsm6 libstdc++-4.8-dev libtiff5 libtsan0 libtxc-dxtn-s2tc0 libumfpack5.6.2 libwebp5 libwebpmux1 libx11-6 libx11-data libx11-xcb1 libxau6 libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-present0 libxcb-sync1 libxcb1 libxdamage1 libxdmcp6 libxext6 libxfixes3 libxi6 libxml2 libxrender1 libxshmfence1 libxslt1.1 libxt6 libxxf86vm1 linux-libc-dev lm-sensors manpages manpages-dev mysql-common nano openssl python python-decorator python-dev python-imaging python-minimal python-numpy python-pil python-pip python-qt4 python-rosdep python-scipy python-sip python-six python-support python-vcstool python2.7 python2.7-dev python2.7-minimal qdbus qtchooser qtcore4-l10n ros-indigo-catkin sgml-base shared-mime-info syslog-ng-core vim wget x11-common xml-core  

***

### Install NASA Debians

Download the following Debians:  
[nasa-indigo-workspace](https://drive.google.com/file/d/0B4Esozi1aH0sZFJPSTVFNy1OM1k/view?usp=sharing)  
[nasa-val-system-config](https://drive.google.com/file/d/0B4Esozi1aH0sLXlYaE5RbnBSWVk/view?usp=sharing)  
[python-pyqtgraph](https://drive.google.com/file/d/0B4Esozi1aH0sZmdOY0dKanlfbzQ/view?usp=sharing)

Navigate to the download location and install the Debians with the following command:

    sudo dpkg -i nasa-indigo-workspace*.deb nasa-val-system-config*.deb python-pyqtgraph*.deb

#### Extra steps for Link Processor or Testbed
If setting up the Link robot processor or a testbed, complete these extra steps. Install the following packages:

    binutils cpp cpp-4.8 dkms fakeroot gcc gcc-4.8 libasan0 libatomic1 libc-dev-bin libc6-dev libcloog-isl4 libfakeroot libgcc-4.8-dev libgmp10 libgomp1 libisl10 libitm1 libjsoncpp-dev libjsoncpp0 liblzo2-2 liblzo2-dev libmpc3 libmpfr4 libquadmath0 libtsan0 linux-libc-dev make manpages manpages-dev patch  

Download the following Debians:  
[Synapse Driver](https://drive.google.com/file/d/0B4Esozi1aH0sLUJvRHhqYkplVWs/view?usp=sharing)  

Navigate to the download location and install the Debian with the following command:

    sudo dpkg -i nasa-robonet-synapse-driver*.deb 

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