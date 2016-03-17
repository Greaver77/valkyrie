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

The schedule file used here is forearm_testbed_left.yaml and it can be found in [nasa_val_config](https://github.com/NASA-JSC-Robotics/nasa_val_config) and looks like the following,

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

[[images/forearm_serials.png]]
