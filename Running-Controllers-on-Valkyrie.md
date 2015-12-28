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

namespace simple_controller
{
   class SimpleController : public controller_interface::Controller<hardware_interface::EffortJointInterface>
   {
   public:
        SimpleController();
        virtual ~SimpleController();

        bool init(hardware_interface::EffortJointInterface* hw, ros::NodeHandle& n);
        void starting(const rost::Time& time);
        void update(const rost::Time& time, const rost::Duration& period);

   private:
        std::vector<hardware_interface::JointHandle> effortJointHandles;
        std::vector<double> buffer_command_effort;
        std::vector<double> buffer_current_positions;
        std::vector<double> buffer_current_velocities;
        std::vector<double> buffer_current_efforts;
   };
}
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

The class declaration occurs next:
```bash
class SimpleController : public controller_interface::Controller<hardware_interface::EffortJointInterface>
```
Here we are creating a class SimpleController which extends the Controller base class. However, we note that the Controller class is type cast as a hardware_interface::EffortJointInterface. Hmm, well that seems strange. What exactly is an EffortJointInterface anyways? Well, this is a peculiar abstraction that comes from the way ros control manages information. The Controller class is actually an extension of the bulkier ControllerBase class (which we will talk about later) and which contains something called RobotHW (or robot hardware). the RobotHW is a collection of containers which are exposed through an interface. That results in every element with a unique data arrangement being exposed as a different interface. For example, joints are an interface, imus are an interface, force torque sensors are an interface, and lasers are an interface (laser interface does not currently exist). In this simple example we are building a controller to command a joint, so typecasting the controller class as an EffortJointInterface ensures that we will only get the containers (also called handles) associated with sending effort commands to joints.

Next, we have the constructor and destructor for the class
```bash
SimpleController();
virtual ~SimpleController();
```
Followed by three methods: init, starting, and update
```bash
bool init(hardware_interface::EffortJointInterface* hw, ros::NodeHandle& n);
void starting(const rost::Time& time);
void update(const rost::Time& time, const rost::Duration& period);
```
These methods overwrite methods in the Controller class allowing them to be called by the interface. The init method upon initializing the controller, and passes a pointer to the EffortJointInterface as well as the NodeHandle so we can get the handle from the joint we want as well as grab parameter information from the node. The starting is called right as the controller is started which allows for nifty things like stopping and starting the controller without having to reinitialize. The update is called each hardware loop and is where the control is done. Well, sometimes it is where the control is done (this will be discussed more in depth later). 

Next, we have the joint handle
```bash
std::vector<hardware_interface::JointHandle> effortJointHandles;
```
This is the container used to store the information about the joint. Then, we define the extra data to locally store joint information
```bash
std::vector<double> buffer_command_effort;
std::vector<double> buffer_current_positions;
std::vector<double> buffer_current_velocities;
std::vector<double> buffer_current_efforts;
```
This is mostly done here as demonstration to make code more legible.

Whew, we finally got through the header file. We can now move on to the source code:
```bash
#include <SimpleController.hpp>

namespace simple_controller
{
   SimpleController::SimpleController()
   {}

   SimpleController::~SimpleController()
   {}

   bool SimpleController::init(hardware_interface::EffortJointInterface* hw, ros::NodeHandle& n)
   {
      effortJointHandles.clear();
      std::vector<std::string> jointNames;

      if(n.getParam("joints", jointNames))
      {   
          if(hw)
          {
             for(unsigned int i=0; i < jointsNames.size(); ++i)
             {
                 effortJointHandles.push_back(hw->getHandle(jointNames[i]));
             }

             buffer_command_effort.resize(effortJointHandles.size(), 0.0);
             buffer_current_positions.resize(effortJointHandles.size(), 0.0);
             buffer_current_velocities.resize(effortJointHandles.size(), 0.0);
             buffer_current_efforts.resize(effortJointHandles.size(), 0.0);
          }
          else
          {
              ROS_ERROR("Effort Joint Interface is empty in hardware interace.");
              return false;
          }
       }
       else
       {
          ROS_ERROR("No joints in given namespace: %s" n.getNamespace().c_str());
          return false;
       }
  
       return true;
   } 

   void SimpleController::starting(const rost::Time& time)
   {
      for(unsigned int i = 0; i < effortJointHandles.size(); ++i)
      {
          buffer_current_positions[i] = effortJointHandles[i].getPosition();
          buffer_current_velocities[i] = effortJointHandles[i].getVelocity();
          buffer_current_efforts[i] = effortJointHandles[i].getEffort();
      }
   }

   void SimpleController::update(const rost::Time& time, const rost::Duration& period)
   {
      for(unsigned int i = 0; i < effortJointHandles.size(); ++i)
      {
          buffer_current_positions[i] = effortJointHandles[i].getPosition();
          buffer_current_velocities[i] = effortJointHandles[i].getVelocity();
          buffer_command_effort[i] = -30*buffer_current_positions[i] - buffer_current_velocities[i];
          effortJointHandles[i].setCommand(buffer_command_effort[i]);
      }   
   }
}
PLUGINLIB_EXPORT_CLASS(simple_controller::SimpleController, controller_interface::ControllerBase)
```