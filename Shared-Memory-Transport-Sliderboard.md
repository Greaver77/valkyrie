# How to use the Shared Memory Transport Sliderboard

###Install Dependencies
Before getting started, make sure you have install the system level dependencies:

    sudo apt-get install qtbase5-dev libyaml-cpp-dev libyaml-cpp libasound2 libasound2-dev

Also make sure you have installed [our code](Get Our Code)


### Step By Step Guide
1. Make sure you have smtcore running and a schedule loaded
2. A GUI will appear when you run ```shared_memory_sliderboard```
3. When a BCF 2000 is attached, the status in the GUI will change to *BCF Connected*.
4. Once the GUI is connected to the board, you are free to attach dials, sliders, and buttons to shared memory variables. When you click "Attach to Variable", a dialog will come up and ask you to type in the shared memory topic name.
5. Update the range for the selected variable you have attached.  To update the ranges, simply type the desired "Min" and "Max" values in the boxes of an element that is attached to a topic and click "Apply Ranges". Depending on the ranges you choose, the sliders may jump a bit.

### Other options
* If you have a configuration that like and would like to return to, you may click the "Save Configuration" button, and a file explorer will come up asking you where you want to save your configuration file and what you want to name it.
* To load a sliderboard configuration, simply click the "Load Configuration" button and navigate to you config file.
* If you want to wipe the sliderboard, you may click the "Reset Sliderboard" button. This will return all sliderboard elements to zero and detach from all shared memory elements.
