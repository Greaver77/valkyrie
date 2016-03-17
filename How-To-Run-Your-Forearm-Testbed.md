[[images/under_construction.png]]

## Prerequisites
- Testbed computer is setup. See how to setup testbed page(ADD LINK TO PAGE)

## Running A Forearm Testbed
It will be described here how to get a forearm testbed into a state that is ready to load your ROS controller. Many of the steps for getting the testbed running are the same for running the whole robot; however, these processes are started and stopped via button clicks in mission control. For testbeds there are no user interfaces(yet) to help out, so most of this is done through the command line. We recommend using [terminator](http://gnometerminator.blogspot.com/p/introduction.html) to help keep them organized!

### Assumptions
- You are running a left forearm. For a right forearm, most of the instructions are the same, just replace 'left' with 'right'.
- You must have our code. You can get it [here](Get Valkyrie Code)
- Your catkin workspace is build and installed. Do this by ```cd ~/val_indigo/ && catkin_make install``` if you have not.

Step one is to start ```smtcore```, so in a terminal execute
```bash
smtcore
```

With ```smtcore``` running, you can now load a schedule file. As I said, this page assumes your running a *left* forearm and the schedule file used here will reflect that. It should be straightforward to infer from this how to get this going for a right forearm(hint: use the forearm_testbed_right.yaml schedule file!).

The schedule file used here is forearm_testbed_left.yaml can be found in [nasa_val_config](https://github.com/NASA-JSC-Robotics/nasa_val_config) and looks like the following,

```yaml
left_arm:
    address: 0
    nodes:
        forearm_sensors: {address: 1, tokens: !include midas.yaml}
        j5: {address: 5, tokens: !include turbo.yaml}
        athena1: {address: 6, tokens: !include athena1.yaml}
        athena2: {address: 7, tokens: !include athena2.yaml}

```

Now the synapse driver can be started which will start data flowing from the hardware to the testbed computer. In another terminal run,

```bash
control <path_to_schedule_file>
```

For the schedule file above that command becomes,

```bash
control -r ~/val_indigo/install/share/nasa_val_config_files/robonet_schedules/forearm_testbed_left.yaml
```

The terminal output from that command should look like,

[[images/RunControl.png]]

The next step involves loading coefficients(coeffs) to the boards that control the forearm actuators. There are 2 [Athena boards](Glossary Of Terms) that control the wrists and fingers as well as a [Leonidas board](Glossary Of Terms) that runs the forearm yaw actuator. To load the correct coeffs, you will need to look on the hardware for the serial numbers of the forearm yaw actuator(v_g_*) and wrist/finger(v_h_*) actuators. Here is an example of what to look for,

[[images/forearmSerials.png]]

Loading coeffs is done with the help of an 'instance file' which describes the actuators on a robot and the serial numbers corresponding to those actuators. You will need to put the serial numbers for your hardware in the file ```~/val_indigo/src/val_description/common/xacro/serial_numbers/forearm_testbench_serials.xacro```. For the serial numbers shown in the  figure above, the file will look like the following,

```xml
<robot xmlns:xacro="http://ros.org/wiki/xacro" name="forearm_testbench">

    <xacro:property name="forearm_yaw_serial_number" value="v_g_016" />
    <xacro:property name="forearm_serial_number" value="v_h_007" />

</robot>
```

These serial numbers correspond to files that contain coeffs specific to these actuators, so it's important you have these correct or you will likely see unpredictable behavior.

Once you have the serial numbers entered into the file, you will need to do a clean build(remove the build devel and install directories in the ~/val_indigo workspace then ```catkin_make install```) in order for the instance file to properly regenerate. You now need to load coeffs to the hardware. This is done in two steps because the Athena boards are done separately from the Leonidas boards. To load coeffs to the Leonidas, in a terminal type

```bash
cfgLoader -i ~/val_indigo/install/share/val_description/instance/instances/instance_files/forearm_testbench.xml
```

In the terminal you will see some log messages that probably tell you unable to load coeffs to Athena actuators or something along those lines. Don't worry about those for this step. The next step will take care of the Athena coeffs. Now in a terminal, execute the following,

```bash
streamFunctions -i ~/val_indigo/install/share/val_description/instance/instances/instance_files/forearm_testbench.xml
```

Now you should see more terminal output telling you it successfully loaded coeffs to the Athena's. The final thing left to do is to start the controller manager. In a terminal executed the following,

```bash
roslaunch val_deploy val_controller_manager.launch model_file:=model/urdf/forearm_left.urdf
```

**Reset Faults**

**Park**

Once the controller manager has started it is waiting for a ROS controller to be loaded. 

**Servo**