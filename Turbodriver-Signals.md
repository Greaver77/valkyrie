### Overview
This page describes all of the signals that are populated by Valkyrie's motor controllers.

### Temperature Sensors
| Name            | Description | Units | Notes |
|-----------------|-------------|-------|-------|
| BridgeTemp_C    | Located on the motor driver bridge circuitry. |   C   |  This sensor will let you know when a driver is overheating.  Overheating is typically caused by running large currents through the driver for an extended amount of time.  Poor airflow across the driver heat sink can cause overheating.  If a bridge overheats only on a particular actuator, please check fans and airflow.     |
| MotorTemp_C     | Located on the motor stator windings.  |  C    | This sensor will let you know when a motor is overheating.      |
| LogicCardTemp_C | Located on the motor drive logic circuitry. |  C     | This sensor gives the best approximation of ambient temperature near the motor driver.  Large temperatures on this sensor implies poor airflow.      |

### Kinematic Variables
Kinematic variables can be configured to use several different inputs or filters.  The following are the recommended and default variables used at the time of writing.

| Name            | Description | Units | Notes |
|-----------------|-------------|-------|-------|
| JointAPS_Angle_Rad | Angular position | radians | Calculated from 13-bit output sensor located at the output of the actuator. |
| JointAPS_Vel_Radps | Angular velocity | radians/sec | Calculated from motor side encoder plus spring deflection sensor.  The velocity calculation is a finite difference on position then filtered using an alpha filter. |
| JointTorque_Meas_Nm | Torque | Nm     | Calculated from 32 bit sensor located across the torsional spring. |

### Electrical Variables
| Name            | Description | Units | Notes |
|-----------------|-------------|-------|-------|
| BusVoltage_V | Motor Bus Voltage at driver | V | Shows if driver is getting motor power.  Can be used to diagnose wiring or power dropouts. |
| Current_Abs_Amps | Driver output current | A | Moving average of absolute value of three phase current output by the motor driver. |

### Health Variables
| Name            | Description | Units | Notes |
|-----------------|-------------|-------|-------|
| Proc_HeartBeat | Driver heart beat |  | Increasing number sent from driver.  Used to ensure comm and driver are active. |
| StatReg1 | Status of driver commands |  |  |
| StatReg2 | Status of driver faults |  |  |

## Forearm Signals

### Forearm Status
|Name      | Description | Units | Notes |
|----------|-------------|-------|-------|
|OT_STATUS | Status of the athena| | Any value other than 0 means that the athena board is faulted, faulting all actuators associated with that board|

### Additional Forearm Topics
|Name      | Description | Units | Notes |
|----------|-------------|-------|-------|
|currentPosRad | Current Angular Position | Rad | Unique to Thumb Roll, gives the current position in Rad as read from the output hall effect sensor|
|Aps1_Raw |Input Encoder Reading |Counts | read from 13-bit position sensor located on input side of motor shaft|
|Aps2_Raw |Output Encoder Reading |Counts | read from 13-bit position sensor located on the output side of pulley motor system|
|ActualDuty | Applied Duty | Percent | Duty percent that is actively applied to the motor|

## Sensor Topics

### IMU Sensor Topics
|Name       | Description | Units | Notes |
|-----------|-------------|-------|-------|
|QuaternionW | w quaternion component | | rotation magnitude of quaternion as read by imu |
|QuaternionX | x quaternion component | | x component of quaternion rotation as read by imu |
|QuaternionY | y quaternion component | | y component of quaternion rotation as read by imu |
|QuaternionZ | z quaternion component | | z component of quaternion rotation as read by imu |
|AngularVelocityX | Imu angular velocity x | rad/s | angular velocity about the body fixed x axis of the imu|
|AngularVelocityY | Imu angular velocity y | rad/s | angular velocity about the body fixed y axis of the imu|
|AngularVelocityZ | Imu angular velocity z | rad/s | angular velocity about the body fixed z axis of the imu|
|LinearAccelerationX | Imu linear acceleration x| m/s^2 | linear acceleration along the body fixed x axis of the imu|
|LinearAccelerationY | Imu linear acceleration y| m/s^2 | linear acceleration along the body fixed y axis of the imu|
|LinearAccelerationZ | Imu linear acceleration z| m/s^2 | linear acceleration along the body fixed z axis of the imu|