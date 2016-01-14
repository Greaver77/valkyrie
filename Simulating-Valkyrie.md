[[images/under_construction.png]]  

# (1-14-2016) - The instructions below will likely be changing frequently as we work to stabilize the Valkyrie sim. If you are interested in using the Gazebo sim for Valkyrie, we advise you to have all Valkyrie repositories on the develop branch and fully up-to-date. 

# Prerequisites
To follow these instructions, you must first have the following:
* Working installation of Simulation Construction Set(SCS [LINK LINK LINK])(Optional of you want to roll your own walking controller)
* Valkyrie Software(get that [here](https://github.com/NASA-JSC-Robotics/valkyrie/wiki/Get-Valkyrie-Code))
* Gazebo 4(Instructions for upgrading from Gazebo 2.x to Gazebo 4.x can be found [here](http://gazebosim.org/tutorials/?tut=ros_wrapper_versions))

# Getting Started
This tutorial details how to get Valkyrie walking around in Gazebo using the walking controller provided by The Florida Institute for Human and Machine Cognition([IHMC](http://robots.ihmc.us/)), and works very much the same as getting the IHMC walking controller running on the real Valkyrie. First, the controller must be deployed to the robot, which in the case of simulation your local machine will be acting as the robot. To deploy IHMC's controller, you will need to add a Run Configuration in Eclipse. To do this, click the dropdown arrow next to the green play button([[images/EclipsePlayButton.png]]) near the top of Eclipse and select 'RunConfigurations...',

[[images/EclipseRunConfigurations.png]]

This will bring up a window where you will need to add a new Gradle Run Configuration. Create a new Run Configuration as shown here:

[[images/AddPublishToValkyrieLocal.png]]

In the **Name** field, you can choose to name the script whatever you like(here we have chosen 'Publish to Valkyrie Local'). In the **Gradle Task** field, you should put ':ValkyrieHardwareDrivers:deployLocal', and in the **Working Directory** field, you should put '${workspace_loc:/_WorkspaceName}' where _WorkspaceName should be replaced with the name of your workspace beginning with an underscore. For example, in the above image, the name of the gradle workspace is 'IHMC_Robotics'; therefore, for the **Working Directory** field I would put '${workspace_loc:/_IHMC_Robotics}'.

Once you have completed the Run Configuration, go ahead and run it, and with any luck, your Eclipse console should out something similar to,

[[images/SuccessfulValkyriePublish.png]]

and you should now have a new directory at ~/valkyrie(/home/user/valkyrie) which contains .jar files for running IHMC's controller.

Now you are ready to launch Valkyrie in Gazebo. Execute the following command in a terminal,

```bash
roslaunch val_gazebo val_sim.launch
```

You may see a number of SDF warnings. These are expected and are not an indicator that something is wrong.

don't worry about these, they are expected and are not reflecting any actual problems. This will bring up a paused Gazebo sim with Valkyrie ready to go.