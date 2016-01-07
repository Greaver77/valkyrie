[[images/under_construction.png]]

This page will go through the full process of turning on the robot and getting everything running so you may run your own ROS controller to move the robot. You should first make sure you are familiar with the terms listed on the [glossary of terms](Glossary Of Terms) page, as this page will use a number of the terms listed there.

##Assumptions##
1. You are running from a source installation. For running from debians, the steps are pretty much exactly the same just without the steps to make sure your catkin workspaces are built/installed

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