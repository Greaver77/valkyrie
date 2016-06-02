[[images/under_construction.png]]

This page needs to contain the instructions for accessing and modifying the IPs of the Multisense.  

##Table of Robot Multisense I.P. Addresses

Listed here is a table of the ip address that is to be used by the Multisense on each Valkyrie Robot.
If you wish to use a Multisense on a current robot, it must have the configuration that corresponds to the robot on the list for which it will be mounted.

Robot|IP Address|Gateway|NetMask
:--------:|:--------:|:---------:|:--------:
Valkyrie A|192.168.1.11|192.168.1.1|255.255.255.0
Valkyrie B|192.168.1.21|192.168.1.1|255.255.255.0
Valkyrie C|192.168.1.31|192.168.1.1|255.255.255.0
Valkyrie D|192.168.1.41|192.168.1.1|255.255.255.0

If you are using an old Multisense unit, or your Multisense ip address does not match the table above the you may follow the next set of directions for setting up your Multisense.

##Configuring your Multisense SL

Every multisense comes with the following ip address configuratoin:

IP Address|Gateway|NetMask|mtu
:-------:|:--------:|:--------:|:--------:|:-----:
10.66.171.21|10.66.171.1|255.255.240.0|7200

If your Multisense sensor is not at the factory default then it should be reset to the factory default (for these instructions, it is possible to change the ip address directly, but it utilizes slightly different commands, and requires that you know the current ip address exactly).

###Resetting to Factory Default

To reset the Multisense to the factory default you need to have a computer that is on the same network of the Multisense (for old Valkyrie multisenses the network it 10.185.0.* with a safe ip address for the computer being something like 10.185.0.110). We also assume that you have installed the ros multisense driver.

To rest the ip address of the device run the command:
####NOTE: This command must be run as root
```
rosrun multisense_lib ChangeIpUtility -b <network interface>
```

Where the <network interface> is the interface that has the connection to the Multisense (usually eth0).

###Set the Multisense to the new ip address

to set the Multisense to the correct ip address, you will first need to change the network to the same on that is used by the Multisense (it is recommended to use 10.66.171.20 for you ip address). Also note the mtu of 7200 that is used by the Multisense.

Once the ip address of the computer talking to the multisense is set up, run the following command:
```
rosrun multisense_lib ChangeIpUtility -A <ip address> -G 192.168.1.1 -N 255.255.255.0
```

where the <ip address> is the address corresponding to the robot in the table that you will be using.

##Hardware wiring

Also need to add pictures/video?/gif of how to route the ethernet cable of the Multisense from the primary onboard switch to Zelda's second NIC.  

## Overview  
As part of the [Cartman Release](Valkyrie-Software-Cartman-Release) we are modifying the connectivity path of the Multisense. This has shown in testing to be more stable and achieve overall better bandwidth.  