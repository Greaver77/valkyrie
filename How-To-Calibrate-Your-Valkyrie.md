# Prerequisites
1. Before calibrating Valkyrie's joints you must have the [Valkyrie software](https://github.com/NASA-JSC-Robotics/valkyrie/wiki/Get-Valkyrie-Code)
2. You must be using the source installation of val_description on the robot, otherwise the updated joint offsets will be lost the next time you update your debian install of val_description and you will need to redo the calibration process
3. You must have logic power on and the actuator coefficients loaded. See [this page](Booting Up Valkyrie) for instructions on how to do this. Make sure to leave the mission control GUI up, you will need it.

# Recommended Tools
* M2-M6 hex drivers. This will cover pretty much all bolts on the robot
* Magnet. Optional but can help prevent screws from falling into hard-to-reach places
* Extreme patience

# Calibrating Valkyrie's Joints
You will first need to remove the soft goods surrounding the joint(s) you are calibrating.
**Put back soft goods after you are done calibrating each joint.  It's easy to lose bolts or damage soft goods if you don't put things back when you are done with them.**

[[images/robot_clothes.png]]

The videos below show how to position each joint for calibration. Before calibrating any one joint, be sure to first check that moving the joint in the positive direction results in an increasing joint position value as reflected by the joint encoder. The joint position value for each joint is reflected on the calibration GUI which can be opened from your ui_builder main window by clicking file->add tab(s)(config file), and navigating to the robot_calibration_val_X.uic where 'X' is the letter corresponding to the robot you are calibrating. You should then see the following window appear,

[[images/CalibrationGUI.png]]

From here, the general workflow while calibrating should look similar to the following:

1. Choose any joint you wish to calibrate

2. Verify moving the joint in the positive direction results in positive motion as reflected by the joint angle on the user interface. If it is backwards, click the 'Flip Joint Direction' button corresponding to the joint you are working with. 

3. Install the calibration fixture for the joint you are installing, or move the joint to it's hard stop if you are calibrating a joint that does not use a fixture. 

4. Click the 'Calibrate Joint' button corresponding to the joint you are calibrating. Hitting this button will kick off a few processes that, after they finish, should result in the joint's position value being updated to the calibrated value. Note that the calibrated value is not necessarily zero.

5. After calibrating your robot, don't forget to create a fork of val_description and put in a pull request to the [NASA val_description repo](https://github.com/NASA-JSC-Robotics/val_description), otherwise your changes will likely get wiped away!

## [Shoulder Pitch](https://www.youtube.com/watch?v=i_R_QV1J_CA)

## [Shoulder Roll](https://www.youtube.com/watch?v=QIns0CLNaQc)

## [Shoulder Yaw](https://youtu.be/vYu5TmopCmc)

## [Elbow Pitch](https://www.youtube.com/watch?v=-FDrI2PnfEU)

## [Forearm Yaw](https://www.youtube.com/watch?v=rJMl_68hfzU&feature=youtu.be)

## Wrist

## [Lower Neck Pitch](https://youtu.be/ociZaKF0tQw)

## [Neck Yaw](https://youtu.be/Kh7yX1gp57s)

## [Upper Neck Pitch](https://www.youtube.com/watch?v=7lFraUiKlNY&feature=youtu.be)

## [Knee Pitch](https://youtu.be/ejU2QimhXzI)

## [Ankle](https://youtu.be/XuRsS6dZCk8)

## [Hips](https://youtu.be/FPSuRZxlhFw)

## [Waist](https://www.youtube.com/watch?v=mTMlzIQrnAw&feature=youtu.be)