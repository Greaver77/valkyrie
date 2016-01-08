First, open a terminal and create a workspace

    mkdir -p ~/val_github_ws/src && cd ~/val_github_ws/src

Set your Github username as an environment variable.  It will make the rest of the instructions easier.

    export GITHUB_USER=<user>

NOTE: replace `<user>` with your Github user name.  You will be prompt to enter your Github password.


Download the workspace file, the install helper, and import the code:

    curl -u $GITHUB_USER -H "Accept: application/vnd.github.raw" "https://api.github.com/repos/NASA-JSC-Robotics/val_workspaces/contents/public_https_full_workspace.yaml?ref=feature/github_workspace" > workspace.yaml
    curl -u $GITHUB_USER -H "Accept: application/vnd.github.raw" "https://api.github.com/repos/NASA-JSC-Robotics/val_workspaces/contents/workspace_checkout?ref=feature/github_workspace" > workspace_checkout
    python workspace_checkout workspace.yaml
