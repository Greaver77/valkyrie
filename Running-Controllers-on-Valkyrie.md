[[images/under_construction.png]]

# So You Want To Make Your Own Controller

The first thing you need to understand for creating your own controller, is the method for interfaceing that controller with the Valkyrie core software. Valkyrie uses ros_control as a method of exposing interfaces to the user as well as well as for loading and unloading controllers. Information on the ros-control archatecture can be found [here](https://github.com/ros-controls). 

#Starting Simple

A good engineer could go through the ros-control documentation and create a control that perfectly integrates itself with the Valkyrie software. However, since you to the time to visit this page maybe we cna shed some extra lite on how to interface your control with Valkyrie. To start, let make a simple controller to control a single joint.

Each controller must be a class which extends one of two possible base classes contained in the control_interface package. The two classes are Controller and ControllerBase. I am going to start with extending Contorller as the ControllerBase class gets a little bit more complicated to explain imediately. Here is an example header file for a simple controller:

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

