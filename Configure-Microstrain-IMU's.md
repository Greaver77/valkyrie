[[images/under_construction.png]]

# Your Microstrain and You

This page gives detailed instructions for configuring the Microstrain IMU's on Val. The configuration resulting from these instructions will return the IMU to the state it should be in when it arrives, however, should you change the configuration these instructions will show you how to return it to the initial configuration. There are 2 flavors of Microstrain IMU's on Val, both the [3DM-GX4-25](http://www.microstrain.com/inertial/3dm-gx4-25) and the [3DM-GX4-15](http://www.microstrain.com/inertial/3dm-gx4-15). 

## Prerequisits
- You must have access to a windows computer and you must have admin privelages
- You have installed the MIP Monitor software. This comes on a blue flash drive with the IMU's. You should have gotten one with your Val. If you did not, please [contact us](Contact Us).
- You have the Microstrain IMU cable that goes from the IMU's 9-pin connector to USB.

## Configuring the IMU
The instructions here are written using a 3DM-GX4-25, however, the instructions for the 3DM-GX4-15 are the same with the exception of the magnetometer stuff.

To get started, plug in your Microstrain IMU to a Windows computer. From the Start menu, open up MIP Monitor,

[[images/ClickMIPMonitor.png]]

A window should pop up, listing the available IMU's that it has found,

[[images/MIPMonitorOpeningScreen.png]]

Your IMU should be listed in the box. Make sure the model and serial numbers listed match your device,

[[images/MIPMonitorOpeningScreenWithArrows.png]]

You must start the device streaming. To do this, simply click the blue play button on the opening screen,

[[images/MIPMonitorClickPlayAnnotated.png]]

After clicking play, the status box should read, 'Streaming Data'. To now configure the settings of the device, click Settings->Device...,

[[images/MIPMonitorClickSettingsDeviceSettings.png]]

The following window will pop up,

[[images/MIPMonitorDeviceSetupIMUTabAnnotated.png]]
[[images/tmp.png]]

**Make sure you are on the IMU tab in Device Setup and NOT the Estimation Filter tab. The Estimation Filter tab should not contain any packet information. If it does, remove it or you will see IMU performance issues.**