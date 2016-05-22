## Pre-requisites:
* SSH keys - Ensure you have a ssh key with [github](https://help.github.com/articles/generating-ssh-keys/)  
  This also means any existing ssh keys on the robot should be removed and replaced with the host teams ssh key.  
* Expected that you will have completed [Setup Valkyrie Developer Environment](Setup-Valkyrie-Developer-Environment)

***

### Setup
Create and init a catkin workspace:  

    mkdir -p ~/val_indigo/src && cd ~/val_indigo/src
    catkin_init_workspace
  
Download the workspace repository to the home directory:  

    git clone -b develop git@github.com:NASA-JSC-Robotics/val_workspaces.git ~/val_workspaces

***

### Download Code
Choose from **one** of the four workspaces below:  

Developer or Testbed Workspace:  

    vcs import --input ~/val_workspaces/public_developer_workspace.yaml ~/val_indigo/src/  

Headless Realtime Robot Workspace:  

    vcs import --input ~/val_workspaces/public_robot_workspace.yaml ~/val_indigo/src/  

Headless Vision Robot Workspace:  

    vcs import --input ~/val_workspaces/public_vision_workspace.yaml ~/val_indigo/src/  

Operator Workstation Workspace:  

    vcs import --input ~/val_workspaces/public_operator_workspace.yaml ~/val_indigo/src/  

Source your completed environment.  

    source ~/.bashrc

*** 

### Final Steps
Run the following line to ensure all dependencies have been resolved.  

If using stable Master release:
    cd ~/val_indigo
    vcs custom --args checkout master
    rosdep install --from-paths src -i -y

If using unstable Develop code:
    cd ~/val_indigo
    vcs custom --args checkout develop
    rosdep install --from-paths src -i -y

### Build
    catkin_make install
    source ~/.bashrc

#### Extra steps for Link/Zelda Processor or Testbed
Do NOT do this step for developer machines or operator workstations. Move the Vanguard init file:  

    sudo cp ~/val_indigo/src/val_vanguard_config/upstart/val-vanguard.conf /etc/init/val-vanguard.conf

***
### Troubleshooting

##### Authentication errors?
Getting authentication errors? Try the following:  

    ssh -T git@github.com

If that didn't come back successful, check the docs: 
[Test the Connection](https://help.github.com/articles/generating-ssh-keys/#step-5-test-the-connection).

If it did, your internet connection may have dropped out. Try downloading things again.

##### val_vision compilation errors
This is a known issue.

    rm -rf ~/val_indigo/src/val_vision

##### Compile errors
* Ensure you are on the proper branch (develop most likely)
* Run the rosdep install line again. Maybe a dependency slipped though the cracks... because gazebo does that.
* Ensure ros-indigo-ros-base (or desktop) is installed

##### libffi Missing error
New bug in paramiko, install libffi-dev to resolve the issue.