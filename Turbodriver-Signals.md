### Overview
This page describes all of the signals that are populated by Valkyrie's motor controllers.

### Temperature Sensors
| Name            | Description | Units | Notes |
|-----------------|-------------|-------|-------|
| BridgeTemp_C    | Located on the motor driver bridge circuitry. |   C   |  This sensor will let you know when a driver is overheating.  Overheating is typically caused by running large currents through the driver for an extended amount of time.  Poor airflow across the driver heat sink can cause overheating.  If a bridge overheats only on a particular actuator, please check fans and airflow.     |
| MotorTemp_C     | Located on the motor stator windings.  |  C    | This sensor will let you know when a motor is overheating.      |
| LogicCardTemp_C | Located on the motor drive logic circuitry. |  C     | This sensor gives the best approximation of ambient temperature near the motor driver.  Large temperatures on this sensor implies poor airflow.      |

### Kinematic Variables
| Name            | Description | Units | Notes |
|-----------------|-------------|-------|-------|
| JointAPS_Angle_Rad | Angular position | radians | Calculated from 13-bit output sensor located at the output of the actuator. |
| JointAPS_Vel_Radps | Angular velocity | radians/sec | Calculated from motor side encoder plus spring deflection sensor.  The velocity calculation is a finite difference on position then filtered using an alpha filter. |
| JointTorque_Meas_Nm | Torque | Nm     | Calculated from 32 bit sensor located across the torsional spring. |

### 