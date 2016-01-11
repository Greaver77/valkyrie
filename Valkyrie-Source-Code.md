There are a few different ways to obtain the source code for Valkyrie, and some of the related tools.

## Get code from Github, using ssh
###Pre-requisites:
You must have a registered ssh key with github.  Check [here](https://help.github.com/articles/generating-ssh-keys/) for help setting that up.  If this is your first time using an ssh-key with github, make to do [Step 5: Test the Connection](https://help.github.com/articles/generating-ssh-keys/#step-5-test-the-connection).  Otherwise, vcstool might fail when trying to import the code.

You will also need [vcstool](https://github.com/dirk-thomas/vcstool).  To install, 

    sudo apt-get install python-vcstool

### Setup
Open a terminal and set your Github username as an environment variable.  It will make the rest of the instructions easier.

    export GITHUB_USER=<user>

**NOTE:** _replace `<user>` with your Github user name._

Create and init a catkin workspace  

    mkdir -p ~/val_github_ws/src && cd ~/val_github_ws/src
    catkin_init_workspace

Download the workspace file and import the code using vcs-tool.  Be sure to enter each line separately.  You will be prompted for your Github password.

    curl -u $GITHUB_USER -H "Accept: application/vnd.github.raw" "https://api.github.com/repos/NASA-JSC-Robotics/val_workspaces/contents/public_full_workspace.yaml?ref=develop" > workspace.yaml

    vcs import --input workspace.yaml


## Get code from Github, using HTTPS
When on-site at JSC, you cannot access Github via ssh.  Instead, you need to use `https://`

Open a terminal and set your Github username as an environment variable.  It will make the rest of the instructions easier.

    export GITHUB_USER=<user>

**NOTE**: _replace `<user>` with your Github user name._

Create and init a catkin workspace  

    mkdir -p ~/val_github_ws/src && cd ~/val_github_ws/src
    catkin_init_workspace

Download the workspace file, the install helper, and import the code.  Be sure to enter each line separately.  You will be prompted for your Github password

    curl -u $GITHUB_USER -H "Accept: application/vnd.github.raw" "https://api.github.com/repos/NASA-JSC-Robotics/val_workspaces/contents/public_https_full_workspace.yaml?ref=develop" > workspace.yaml

    curl -u $GITHUB_USER -H "Accept: application/vnd.github.raw" "https://api.github.com/repos/NASA-JSC-Robotics/val_workspaces/contents/workspace_checkout?ref=develop" > workspace_checkout

    python workspace_checkout workspace.yaml


**NOTE**: _One big downside to this approach is that the vcstool does not handle multiple repo authentication very well.  Subsequent calls like `vcs pull` causes a bit of a mess on the console._