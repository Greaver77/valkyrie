# How to use the Shared Memory Transport Sliderboard

###Install Dependencies
Before getting started, make sure you have install the system level dependencies:

    sudo apt-get install qtbase5-dev libyaml-cpp-dev libyaml-cpp libasound2 libasound2-dev

Also make sure you have installed [our code](Get Our Code)


### Make sure your val_indigo workspace is built
```bash
cd ~/val_indigo && catkin_make install
```
### Start SMT Core
Start smt_core by executing the following command in a terminal,

```bash
smt_core
```

### Load your desired schedule file
See the [forearm testbed](How To Run Your Forearm Testbed) for more detail on what is meant by 'schedule file',
```bash
cd ~/val_indigo
control -r <path_to_your_schedule_file>
```

### Start the sliderboard application
You can start it in one of two ways: with rosrun,
```bash
rosrun shared_memory_transport_sliderboard smt_sliderboard
```

or just run the executable
```bash
cd ~/val_indigo
./install/lib/shared_memory_transport_sliderboard
```

After launching the application you should see the following user interface,

[[images/sliderboard.png]]

If your sliderboard is not connected and turned on when you start the UI, the status box will say 'Disconnected'. Once plugged in and powered on it should dynamically update and say 'Connected'.

### Attach to topics
The first step is to click the 'Attach To Variable' button next to a dial, button, or slider that you would like to map to a shared memory topic. A dialog box will pop up asking for the name of the desired topic,

[[images/AttachToVariable.png]]

Note that when you initially attach to a topic, the 'Min' and 'Max' values will be set to the current value, so moving the slider will not vary the value. 

### Set topic ranges
Once you have attached sliders and dials to the desired topics, you should now set the desired Min/Max values. Simply click in the Min/Max text boxes beneath the dials and sliders and set the value. To actually apply the ranges, either click the 'Apply Ranges' button or use the keyboard shortcut 'Ctrl+a'. Once you apply the ranges, the sliders/dials on the board will jump in place to prevent the current value from changing. 

Keep in mind that buttons can only take the value 0 or 1. 

### Reset Sliders
If you would like to wipe the board clean of all topics and ranges, click the 'Reset Sliderboard' button or use the keyboard shortcut 'Ctrl+r' and all sliders/dials will return to zero and all topics/limits will be wiped clean.

### Save a configuration
If you have a sliderboard configuration that you would like to be able to return to quickly, you may save a configuration by clicking the 'Save Configuration' button or through the keyboard shortcut 'Ctrl+s' and a file window will appear asking for the desired save location.

### Load configuration
To load a saved configuration, click the 'Load Configuration' button or press the keyboard shortcut 'Ctrl+o' to bring up a file window. Simply navigate to your saved configuration file and the sliderboard will populate the sliders/knobs will all the data in your configuration file.
