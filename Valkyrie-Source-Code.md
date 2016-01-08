There are a few different ways to obtain the source code for Valkyrie, and some of the related tools.

## Get code from Github, using HTTPS
When on-site at JSC, you cannot access Github via ssh.  Instead, you need to use `https://`

Open a terminal and set your Github username as an environment variable.  It will make the rest of the instructions easier.

    export GITHUB_USER=<user>

NOTE: replace `<user>` with your Github user name.  You will be prompt to enter your Github password.

Create and init a catkin workspace  

    mkdir -p ~/val_github_ws/src && cd ~/val_github_ws/src
    catkin_init_workspace`

Download the workspace file, the install helper, and import the code.  Be sure to enter each line separately.  You will be prompted for your Github password

    curl -u $GITHUB_USER -H "Accept: application/vnd.github.raw" "https://api.github.com/repos/NASA-JSC-Robotics/val_workspaces/contents/public_https_full_workspace.yaml?ref=feature/github_workspace" > workspace.yaml

    curl -u $GITHUB_USER -H "Accept: application/vnd.github.raw" "https://api.github.com/repos/NASA-JSC-Robotics/val_workspaces/contents/workspace_checkout?ref=feature/github_workspace" > workspace_checkout

    python workspace_checkout workspace.yaml


NOTE: One big downside to this approach is that the vcs-tool does not handle multiple repo authentication very well.