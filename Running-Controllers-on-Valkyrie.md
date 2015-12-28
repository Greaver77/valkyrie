[[images/under_construction.png]]

# So You Want To Make Your Own Controller

The first thing you need to understand for creating your own controller, is the method for interfacing that controller with the Valkyrie core software. Valkyrie uses ros_control as a method of exposing interfaces to the user as well as well as for loading and unloading controllers. Information on the ros-control architecture can be found [here](https://github.com/ros-controls). 

#Starting Simple

A good engineer could go through the ros-control documentation and create a control that perfectly integrates itself with the Valkyrie software. However, since you to the time to visit this page maybe we can shed some extra lite on how to interface your control with Valkyrie. To start, let make a simple controller to control a single joint.

Each controller must be a class which extends one of two possible base classes contained in the control_interface package. The two classes are Controller and ControllerBase. I am going to start with extending Contorller as the ControllerBase class gets a little bit more complicated to explain immediately. Here is an example header file for a simple controller:

```bash
#ifndef SIMPLE_CONTROLLER_HPP
#define SIMPLE_CONTROLLER_HPP

#include <hardware_interface/joint_command_interface.h>
#include <controller_interface/controller.h>
#include <pluginlib/class_list_macros.h>
#include <ros/node_handle.h>

class SimpleController : public controller_interface::Controller<hardware_interface::EffortJointInterface>
{
public:
	SimpleController();
	virtual ~SimpleController();

	boot init(hardware_interface::EffortJointInterface* hw, ros::NodeHandle& n);
	void starting(const rost::Time& time);
	void update(const rost::Time& time, const rost::Duration& period);

private:

	std::vector<double> buffer_command_efforts;
	std::vector<double> buffer_current_positions;
	std::vector<double> buffer_current_velocities;
	std::vector<double> buffer_current_efforts;
};

#endif
```
Hmm, that looks like a lot of information to take in at once. Lets see if we can break down what is happening. Lets start with what is being included. The first thing included is

```bash
#include <hardware_interface/joint_command_interface.h>
```
This is the base class for the command type interface which contains methods for sending commands to joints as well as getting some information from joints. We will explore some of these methods later, but for now we just need to include the header for these interfaces. The next thing included is
```bash
#include <controller_interface/controller.h>
```
This is the base class mentioned briefly earlier. We will be brief here as well and move on the the next thing (we will explain the base class thing a little bit). The next two things included are
```bash
#include <pluginlib/class_list_macros.h>
#include <ros/node_handle.h>
```
The node_handle.h most likely means we will be running this code form a ros node and so I will eventually want information from that node. As for the pluginlib, well that is a little more complicated. If you aren't fully familiar with plugins, it essentially is a class that we can "plug in" to running code. The cool thing about this is that the code doesn't need to know the class being plugged in a build. Instead, it only needs to know the base class that is extended by the plugin. That means the robot software doesn't need to know your controller until runtime, and all you need to do is extend a based class that is know to the software, like controller.h. Cool, right? No? Ok, moving on.

