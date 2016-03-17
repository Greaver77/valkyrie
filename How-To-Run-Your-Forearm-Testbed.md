[[images/under_construction.png]]

## Prerequisites
- Testbed computer is setup. See how to setup testbed page(ADD LINK TO PAGE)

## Running A Forearm
It will be described here how to get a forearm testbed into a state that is ready to load your ROS controller. Many of the steps for getting the testbed running are the same for running the whole robot; however, these processes are started and stopped via button clicks in mission control. For testbeds there are no user interfaces(yet) to help out, so most of this is done through the command line.

### Assumptions
- You are running a left forearm. For a right forearm, most of the instructions are the same, just replace 'left' with 'right'.
- You must have our code. You can get it [here](Get Valkyrie Code)
- Your catkin workspace is build and installed. Do this by ```cd ~/val_indigo/ && catkin_make install``` if you have not

Step one is to start ```smtcore```, so in a terminal execute

