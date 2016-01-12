[[images/under_construction.png]]

This page will go through the full process of turning on the robot and getting everything running so you may run your own ROS controller to move the robot. You should first make sure you are familiar with the terms listed on the [glossary of terms](Glossary Of Terms) page, as this page will use a number of the terms listed there.

##Assumptions##
1. You are running from a source installation. For running from debians, the steps are pretty much exactly the same just without the steps to make sure your catkin workspaces are built/installed

2. You know your robot's IP address. This documentation will refer to your robots IP addresses as 'Link-IP' for the IP address of the Link computer and 'Zelda-IP' for the IP address of the Zelda computer.

##Power On Valkyrie##

The first step in powering on the robot is to turn on the power sources. These are located in your juice box. To turn them on, flip the switches on both the low voltage and high voltage sources to on. Once the LED display reads "OFF"(should take a couple seconds) you can press the "OUT" button which will fully start the power source. The image below shows the buttons you will need to press.

[[images/JuiceBoxButtons.png]]

Now that the power sources are running, you can now turn the robot on. Do this by pressing the button that is located behind the right shoulder of the robot as shown in the figure below.

[[images/RobotPowerButton.png]]

The button will have a blue glow, and the light in Valkyrie's chest should "beach ball",

[[images/Ring_LED/rainbow.gif]]

After "beach balling" for ~10 seconds, it should turn red,

[[images/Ring_LED/no_comm.gif]] 

Once the light is spinning red, you are ready to get going on the computers. On your operator computers, if you aren't sure if your catkin workspace is built, go ahead and do that,

```bash
cd ~/val_indigo 
catkin_make install
```

Now do the same for the workspaces on Link. You will need to ssh into the Link computer to do this, so in a terminal,

```bash
ssh -YC val@'Link-IP'
cd ~/val_indigo
catkin_make install
```

Now from the operator computer, open ui_builder,

```bash
ui_builder &
```
this will bring up a blank ui_builder window,

<img src="https://github.com/NASA-JSC-Robotics/valkyrie/wiki/images/ui_builder.png" width="250">  

from here you can add the 'mission_control' tab corresponding to your robot. On the ui_builder window, click file->add tab(s)(config file). It will open a file browser where you can navigate to and open the mission_control_val_X.uic that corresponds to your robot. If you are running unit C, then you will open the file 'mission_control_val_C.uic'. In your ui_builder window you should then see,

[[images/MissionControl.png]]

After opening the mission control GUI, the first thing you will want to do is click the "Be A Robot" button. This button does a number of things:

1. Starts remote [shared memory transport](Shared Memory Transport)(SMT) processes on the robots computers that allow data from the robot to be accessed from remote machines
2. Starts SMT processes on the local machine that look for remotes that are publishing shared memory 

A few seconds after clicking the "Be A Robot" button, the status box labeled "Robot" on the top right should turn green.

[[images/ClickBeARobot.png]]

The next step is to start the controller manager. This is done by clicking the 'Controller Manager : Start' button. After a few seconds, the status button on the top right should turn green, indicating the controller manager is up and running,

[[images/ClickControllerManagerStart.png]]

**Note that starting the controller manager also starts a mode controller. This is important because if you do not have the controller manager running, any actions that use the controller manager such as clearing faults or resetting actuator estops will fail because they rely on the mode controller.**

