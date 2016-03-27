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

[[images/Sliderboard.png]]

5. Once the GUI is connected to the board, you are free to attach dials, sliders, and buttons to shared memory variables. When you click "Attach to Variable", a dialog will come up and ask you to type in the shared memory topic name.
6. Update the range for the selected variable you have attached.  To update the ranges, simply type the desired "Min" and "Max" values in the boxes of an element that is attached to a topic and click "Apply Ranges". Depending on the ranges you choose, the sliders may jump a bit.

### Other options
* If you have a configuration that like and would like to return to, you may click the "Save Configuration" button, and a file explorer will come up asking you where you want to save your configuration file and what you want to name it.
* To load a sliderboard configuration, simply click the "Load Configuration" button and navigate to you config file.
* If you want to wipe the sliderboard, you may click the "Reset Sliderboard" button. This will return all sliderboard elements to zero and detach from all shared memory elements.
