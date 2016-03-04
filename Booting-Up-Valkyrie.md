This page will go through the full process of turning on the robot and getting everything running so you may run your own ROS controller to move the robot. You should first make sure you are familiar with the terms listed on the [glossary of terms](Glossary Of Terms) page, as this page will use a number of the terms listed there.

##Assumptions##
1. You are running from a source installation. For running from debians, the steps are pretty much exactly the same just without the steps to make sure your catkin workspaces are built/installed

2. You know your robot's IP address. This documentation will refer to your robots IP addresses as 'Link-IP' for the IP address of the Link computer and 'Zelda-IP' for the IP address of the Zelda computer.

For any issues that may arise that are not addressed here, please see the [trouble shooting page](Trouble Shooting)

##Power On Valkyrie##

The first step in powering on the robot is to turn on the power sources. These are located in your juice box. To turn them on, flip the switches on both the low voltage and high voltage sources to on. Once the LED display reads "OFF"(should take a couple seconds) you can press the "OUT" button which will fully start the power source. The image below shows the buttons you will need to press.

[[images/JuiceBoxButtons.png]]

Now that the power sources are running, you can now turn the robot on. Do this by pressing the button that is located behind the right shoulder of the robot as shown in the figure below.

[[images/RobotPowerButton.png]]

The button will have a blue glow, and the light in Valkyrie's chest should start to "beach ball",

[[images/Ring_LED/rainbow.gif]]

Once the light is "beach balling", you are ready to get going on the computers. On your operator computers, if you aren't sure if your catkin workspace is built, go ahead and do that,

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
3. Checks if the PDBMTI(a.k.a the power distribution board) has firmware, if not it will flash firmware to the PDBMTI. If it is already loaded it will simply move on. 

**NOTE**: PDBMTI firmware is only flashed one time once the robot is turned on. It will not be done again until the robot is turned completely off.

A few seconds after clicking the "Be A Robot" button, the status box labeled "Robot" on the top right should turn green.

[[images/ClickBeARobot.png]]

You should also see the light on Valkyrie's chest turn white,

[[images/Ring_LED/idle.gif]]

The next step is to start the controller manager. This is done by clicking the 'Controller Manager : Start' button. After a few seconds, the status button on the top right should turn green, indicating the controller manager is up and running,

[[images/ClickControllerManagerStart.png]]

**Note that starting the controller manager also starts a mode controller. This is important because if you do not have the controller manager running, any actions that use the mode controller, such as clearing faults or resetting actuator estops, will fail because they rely on the mode controller.**

After starting the controller manager, you can turn on logic power by clicking the 'Logic Power: On' button. 

[[images/ClickLogicPowerOn.png]]

This will also turn the light in the center of the chest green and should look something like,

[[images/Ring_LED/logic_power.gif]]

Logic power is the low voltage(12 volt) BUS that provides power to the various circuit boards and motor controllers for the joints. After clicking this button, a number of things will take place in addition to turning on logic power, so be patient as it may take 20-30 seconds to finish. After the boards are powered, actuator coefficients are loaded to each board. It will also attempt to clear all actuator faults and 'Park' the actuators, which is a term we use for referring to a state where the actuators are safe and unable to commutate. 

You should get log messages in the log window an the bottom of the UI that let you know the status of actuator coeff loading and various other processes, but visually you can check that the actuators are alive by opening up the status user interfaces(ADD LINK TO UI's). In the 'robot_status' UI you will see each joint's position, velocity, effort, temperature, etc. If the actuator coeffs fail to load or logic power is not on, then you will not see actuator/joint data.

With logic power on, the only things left to do before moving the robot is to turn on high voltage(we refer to this as motor power) and to servo the actuators. Simply click the "Motor Power: On" button,

[[images/ClickMotorPowerOn.png]]

Assuming the e-stop is not pressed and the high voltage power supply is on, the light in the chest should turn purple,

[[images/Ring_LED/purple.gif]]

While the chest light is purple the power system is charging capacitors(caps), and the robot will not be servoable because the power system is preventing each [turbodriver](Glossary Of Terms) from clearing it's e-stop. After the caps are done charging, the light will turn blue, indicating that motor power is on,

[[images/Ring_LED/royal_blue.gif]]

**Be extra careful when approaching the robot when the chest light is blue. When the light is blue, there MUST be designated person holding the e-stop. Furthermore, the person holding the e-stop is not to step inside the robots workspace.**

Once motor power is on, the robot is servoable. You can servo the robot via the mission control UI by clicking the servo buttons for either individual limbs or for the entire robot, or by using the mode controller. It is not advisable that you servo the robot without a controller running that will control the robots configuration. Without first running a controller, servoing the actuators will put them in zero force mode which can damage the robot some of the actuators may run away.

If you don't have a controller of your own that you would like to run IHMC's whole body controller, see their wiki [here](http://ihmcrobotics.github.io/) or we have put a quick page together [here](Editing Getting Valkyrie Walking With IHMC's Controller), however, IHMC's wiki is the recommended place to look for instructions on using their software or IHMC's wiki.