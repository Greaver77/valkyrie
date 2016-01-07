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
        void stopping(const ros::Time& time);

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
Followed by four methods: init, starting, update, and stopping
```bash
bool init(hardware_interface::EffortJointInterface* hw, ros::NodeHandle& n);
void starting(const rost::Time& time);
void update(const rost::Time& time, const rost::Duration& period);
void stopping(const ros::Time& time);
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

   void SimpleController::update(const ros::Time& time, const rost::Duration& period)
   {
      for(unsigned int i = 0; i < effortJointHandles.size(); ++i)
      {
          buffer_current_positions[i] = effortJointHandles[i].getPosition();
          buffer_current_velocities[i] = effortJointHandles[i].getVelocity();
          buffer_command_effort[i] = -30*buffer_current_positions[i] - buffer_current_velocities[i];
          effortJointHandles[i].setCommand(buffer_command_effort[i]);
      }   
   }

   void SimpleController::stopping(const ros::Time& time)
   {}
}
PLUGINLIB_EXPORT_CLASS(simple_controller::SimpleController, controller_interface::ControllerBase)
```
Lets go over the components of this code. First we have the constructor and destructor functions
```bash
SimpleController::SimpleController()
{}

SimpleController::~SimpleController()
{}
```
Nothing really to go over here as they don't really do anything special in this case. Next we hop into to init function
```bash
 bool SimpleController::init(hardware_interface::EffortJointInterface* hw, ros::NodeHandle& n)
```
We start the init function by clearing the vector of joint handles, and declaring a vector (or list) used to store the joint names we will be using
```bash
effortJointHandles.clear();
std::vector<std::string> jointNames;
```
So, now we need to actually get the names of the joints we will use as that is how we get the handles (those containers with the data we need). In this case we will try to get them form the node parameter "joints" with the line
```bash
if(n.getParam("joints", jointNames))
```
This method is nice in that it allows us to put the joints used by the controller in a configuration file, meaning we could use the same controller source code that each grab different joint resources. Alternatively, if we just want the names of all handles owned by the chosen interface you can request that, but we will talk more about that later (when we have more interfaces to deal with).

Once we have the names of the joints we want to use we do a quick check to make sure that the interface isn't empty before we start trying to grab the handles with
```bash
for(unsigned int i=0; i < jointsNames.size(); ++i)
{
   effortJointHandles.push_back(hw->getHandle(jointNames[i]));
}
```
The member function getHandle trys, as the name implies, to get a handle with a given name (in this case the name is the ith element of the vector jointNames). This does mean that we need the names we chose in the "joints" parameter to match some, or all, of the names used to make the handles. In the case of Valkyrie, the names used to make joint handles are the names of the joints in the urdf (created by the val_description package). Once we have the exact size of the data we will be using (basically the number of handles we actually get) then we preallocate space for any variables used:
```bash
buffer_command_effort.resize(effortJointHandles.size(), 0.0);
buffer_current_positions.resize(effortJointHandles.size(), 0.0);
buffer_current_velocities.resize(effortJointHandles.size(), 0.0);
buffer_current_efforts.resize(effortJointHandles.size(), 0.0);
```  
We note that the init function returns one of two values. It returns "true" if everything finished properly, or "false" if there were any issues. If the init function returns false, then your controller will not run.

After the init function (and assuming that init didn't return false for whatever reason), we have the starting function
```bash
void SimpleController::starting(const rost::Time& time)
``` 
For the starting function we have chosen to loop through the list of current positions, velocities, and efforts of the joints we are using, and to get the current values from the hardware at the time of starting
```bash
for(unsigned int i = 0; i < effortJointHandles.size(); ++i)
{
    buffer_current_positions[i] = effortJointHandles[i].getPosition();
    buffer_current_velocities[i] = effortJointHandles[i].getVelocity();
    buffer_current_efforts[i] = effortJointHandles[i].getEffort();
}
```
We see that we use a get function to get values form the handle. The get functions owned by each handle depends on the interface the handle is associated with. In the case of joints we can get position, velocity, effort, and the name (of the joint).

After the controller has started, the update 
```bash
void SimpleController::update(const rost::Time& time, const rost::Duration& period)
```
will be called periodically by the Valkyrie software.

**Important: the Valkyrie core software runs a 500 hz loop, and the update function of EVERY controller is called ONCE each loop**

The Update in this case runs a simple PD controller about 0 position, 0 velocity with a position gain of 30 and a derivative gain of 1.
```bash
for(unsigned int i = 0; i < effortJointHandles.size(); ++i)
{
   buffer_current_positions[i] = effortJointHandles[i].getPosition();
   buffer_current_velocities[i] = effortJointHandles[i].getVelocity();
   buffer_command_effort[i] = -30*buffer_current_positions[i] - buffer_current_velocities[i];
   effortJointHandles[i].setCommand(buffer_command_effort[i]);
}  
```
The setCommand function allows you to write information through the interface to the hardware. Not every handle has a set function (in face most do not). 

After the update, we have the stopping function. This is where we add anything that we want to stop before stopping the controller. The advantage of this is we can stop a controller, and then start it again without ever destructing the controller.
```bash
void SimpleController::stopping(const ros::Time& time)
{}
```
The final line of code
```bash
PLUGINLIB_EXPORT_CLASS(simple_controller::SimpleController, controller_interface::ControllerBase)
```
allows us to set up the class as a plugin with the base class, controller_interface::ControllerBase, being the class used by the Valkyrie software to load the plugin.

Now that we have gotten through the source code we now need to figure out how to get the controller loaded into the Valkyrie software. Maybe you want to take a break before we do. Maybe you just want to dive right into it. Either way, it is next.

#Spawning The Simple Controller
Alright, so we have the source code to set up a simple controller and now we need to setup the configuration as well as get the controller to be loaded by the software. To start, lets finish the necessary steps for making the controller a plugin. More information on pluginlib can be found [here](http://wiki.ros.org/pluginlib).

The first addition we need to make the simple controller a plugin is an additional file in the package directory called something like, simplecontroller.xml. The contents of this xml file will be
```bash
<library path="lib/libsimple_controller">
  <class name="simple_controller/SimpleController" type="simple_controller::SimpleController" base_class_type="controller_interface::ControllerBase">
    <description>
      A simple test controller for ros control
    </description>
  </class>
</library>
```
The "lib/libsample_controller" is the library created by your package. Here we have given the plugin the name "simple_controller/SimpleController" which will be important later. Now that we have an xml file that tells us what the name of the plugin, and in what library its source is in, we need to export this for other packages to access. To do this we add the following to the package.xml file:
```bash
<export>
  <controller_interface plugin="${prefix}/simplecontroller.xml"/>
</export>
```
This tells us that the base class plugin is contained in the controller_interface package, and the information on the plugin is contained in the simplecontroller.xml file.

With the plugin defined we will now setup the configuration file for the controller. To do this we start by making a file called "simple_val_knee.yaml". This file will give tell us which joints we will control (spoilers, it is likely a knee) as well as give a separate name for the controller to be used by ros. The contents of the file are as follows
```bash
simple_val_knee:
    type: simple_controller/SimpleController
    joints:
        - rightKneePitch
        - leftKneePitch
```
Looking through the file we have the controller is "simple_val_knee", uses the simple_controller/SimpleController plugin, and is controlling both the rightKneePitch and the leftKneePitch. Now that we have the config file setting the configuration of the robot, we can build the launch file for ros
```bash
<launch>

  <!-- Load joint controller configurations from YAML file to parameter server -->
  <rosparam file="$(find simple_controller)/config/simple_val_knee.yaml" command="load"/>

  <!-- load the controllers -->
  <node name="controller_spawner" pkg="controller_manager" type="spawner" respawn="false" output="screen" args="simple_val_knee"/>

</launch>
```
Here we start by loading the configuration file to the rosparmeters with
```bash
<rosparam file="$(find simple_controller)/config/simple_val_knee.yaml" command="load"/>
```
Then, we use a controller_spawner to spawn our controller as defined in the parameter list with
```bash
<node name="controller_spawner" pkg="controller_manager" type="spawner" respawn="false" output="screen" args="simple_val_knee"/>
```
The spawner uses the ros control architecture to load the controller named in the args (which we associated with a plugin through our config file). When the controller_spawner is stopped, it attempts to unload the controller during the teardown.

Well, thats it. All you need to do is rolaunch the launch file with the controller_spawner, and the simple controller will be loaded and run through the Valkyrie core software. Baring, of course, that the Valkyrie software is running (no software, no control). However, you may have noticed a few undesired traits of the simple example that will not work for more complex controller. Traits such as, being typecast to a single type of interface. Also, being constrained to the loop rate of the Valkyrie core software (which may be too fast for more complex control regimes). We will address some of these issues in the next.

#More Advance Controllers

From the previous controller, we see that the controllers we write are strongly typed. This is good as it lets the api determine the types of controllers being loaded. However, it can be annoying for writing a controller if you want to get more than one type of resource (say, for example, you want to read force sensors and output joint torques in one controller). Luckily there are workarounds, one of which we will cover here.

To get multiple interfaces, we must first fully understand what is happening in the Controller class, the ControllerBase class which is extended by the Controller class, and how they interact with the hardware api. The api uses plugins to load the controllers using the ControllerBase class. A series of request functions then are used to call the virtual methods of starting, init, update, and stoping (called startRequest, initRequest, updateRequest, and stopRequest respectively).  Fortunately for us, we determine which interfaces to grab through the init (or initRequest) and the initRequest happens to be virtual in the ControllerBase class. So, lets rewrite the SimpleController header file that uses the initRequest instead of the init function:
```bash
#ifndef SIMPLE_CONTROLLER_HPP
#define SIMPLE_CONTROLLER_HPP

#include <hardware_interface/joint_command_interface.h>
#include <hardware_interface/imu_sensor_interface.h>
#include <hardware_interface/force_torque_sensor_interface.h>
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

        void starting(const rost::Time& time);
        void update(const rost::Time& time, const rost::Duration& period);
        void stopping(const ros::Time& time);
   
   protected:        
        virtual bool initRequest(hardware_interface::RobotHw* robot_hw, 
                         ros::NodeHandle& root_nh, ros::NodeHandle& controller_nh, 
                         std::set<std::string>& claimed_resources) overide;

   private:
        std::map<std::string, hardware_interface::JointHandle> effortJointHandles;
        std::map<std::string, hardware_interface::ImuSensorInterface> imuSensorHandles;
        std::map<std::string, hardware_interface::ForceTorqueSensorInterface> forceTorqueHandles;
        std::map<std::string,double> buffer_command_effort;
        std::map<std::string, double> buffer_current_positions;
        std::map<std::string, double> buffer_current_velocities;
        std::map<std::string, double> buffer_current_efforts;
   };
}
#endif
```
Notice that in addition to using the initRequest function (which is protected) we are adding two additional handles (imu and force torque sensors). So, how does the initRequest get the interfaces? Well lets look at the implementation of the function:
```bash
bool SimpleController::initRequest(hardware_interface::RobotHw* robot_hw, 
                         ros::NodeHandle& root_nh, ros::NodeHandle& controller_nh, 
                         std::set<std::string>& claimed_resources)
{
    // check if construction finished cleanly
    if (state_ != CONSTRUCTED){
      ROS_ERROR("Cannot initialize this controller because it failed to be constructed");
      return false;
    }

    // get a pointer to the hardware interface
    hardware_interface::EffortJointInterface* effort_hw = robot_hw->get<hardware_interface::EffortJointInterface>();
    if (!effort_hw)
    {
      ROS_ERROR("This controller requires a hardware interface of type hardware_interface::EffortJointInterface.");
      return false;
    }

    // return which resources are claimed by this controller
    effort_hw->clearClaims();


    hardware_interface::InterfaceResources iface_res(getHardwareInterfaceType(), hw->getClaims());
    claimed_resources.assign(1, iface_res);
    hw->clearClaims();

    // success
    state_ = INITIALIZED;
    return true;
}
```
