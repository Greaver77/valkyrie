## Pre-requisites:
SSH keys - Ensure you have a ssh key with [github](https://help.github.com/articles/generating-ssh-keys/)  

You will need [vcstool](https://github.com/dirk-thomas/vcstool).  To install: 

    sudo apt-get install python-vcstool

***

### Setup
Create and init a catkin workspace:  

    mkdir -p ~/val_indigo/src && cd ~/val_indigo/src
    catkin_init_workspace
  
Download the workspace repository to the home directory:  

    git clone -b develop git@github.com:NASA-JSC-Robotics/val_workspaces.git ~/val_workspaces

***

### Download Code

    vcs import --input ~/val_workspaces/public_full_workspace.yaml ~/val_indigo/src/


*** 

### Final Steps
Run the following line to ensure all dependencies have been resolved.

    cd ~/val_indigo
    vcs custom --args checkout develop
    rosdep install --from-paths src -i -y

***
### Troubleshooting
Getting authentication errors? Try the following:  

    ssh -T git@github.com

If that didn't come back successful, check the docs: 
[Test the Connection](https://help.github.com/articles/generating-ssh-keys/#step-5-test-the-connection).