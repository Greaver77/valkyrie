# Your Microstrain and You

This page gives detailed instructions for configuring the Microstrain IMU's on Val. The configuration resulting from these instructions will return the IMU to the state it should be in when it arrives, however, should you change the configuration these instructions will show you how to return it to the initial configuration. There are 2 flavors of Microstrain IMU's on Val, both the [3DM-GX4-25](http://www.microstrain.com/inertial/3dm-gx4-25) and the [3DM-GX4-15](http://www.microstrain.com/inertial/3dm-gx4-15). 

## Prerequisits
- You must have access to a windows computer and you must have admin privelages
- You have installed the MIP Monitor software. This comes on a blue flash drive with the IMU's. You should have gotten one with your Val. If you did not, please [contact us](Contact Us).
- You have the Microstrain IMU cable that goes from the IMU's 9-pin connector to USB.

**Note: Some of the text in the MIP Monitor UI's may differ slightly from the images seen here. This is likely due to different versions of the MIP Monitor software. It should, however, be very similar and close enough to get you through the configuration process. If you have questions, feel free to [contact us](Contact Us)**

If you already know what your doing and don't need a full walkthrough, the following table displays the settings needed that differ from the default,

| | Pelvis Rear IMU|Pelvis Middle IMU|Torso IMU|
|:-:|:-------------:|:---------------:|:-------:|
| Orientation Rate | 250Hz | 250Hz | 250Hz |

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

**Make sure you are on the IMU tab in Device Setup and NOT the Estimation Filter tab. The Estimation Filter tab should not contain any packet information. If it does, remove it or you will see IMU performance issues.** If the packets listed in the IMU tab are empty, add the packets shown in the above filter and have each of them run at 250Hz. If they match what is in the figure, no need to do anything. 

Now click on the 'Low Pass Filter 1' tab. If you have a GX4-15 model, it may just be labeled 'Low Pass Filter',

[[images/MIPMonitorDeviceSetupLowPassFilter1Tab.png]]

Configure both the Accel and Gyro filters to filter at 50Hz.  **If** you have a GX4-25, click the 'Low Pass Filter 2' tab, and configure the filter on the Mag to also filter at 50Hz,

[[images/MIPMonitorDeviceSetupLowPassFilter2Tab.png]]

If you have a GX4-15, then you do not have a mag and you can skip this step. Now you need to set the baud rate. You may exit out of this window and go back to the main MIP Monitor window. To set the baud rate, click Settings->System...,

[[images/MIPMonitorClickSettingsSystemSettings.png]]

This will bring up a window listing the baud rate. Change it to 921600,

[[images/MIPMonitorSystemSettings.png]]

If you would like to capture the gyro bias, make sure the IMU is absolutely still and click Settings->Capture Gyro Bias...,

[[images/MIPMonitorCaptureGyroBias.png]]

Finally, you need to tell the IMU to save the settings otherwise they will be gone once power is removed. Simple click Settings->Save Current Settings...,

[[images/MIPMonitorSaveSettings.png]]

Now you can click the stop button to stop the device streaming and you are done,

[[images/MIPMonitorStop.png]]