## What happens if you want to back up your current env?

Because a lot of the dependencies are Debian based and frankly there isn't a great way to roll back Debians, there will always be risk to trying an upgrade. However we can at least snapshot you're environment variables and repositories so that we have a place to start if a roll-back is required.  

Run the following commands on every system. (Link/Zelda/Workstation/etc).

Repeat this command for *each* catkin workspace you have.

    cd ~/my_favorite_catkin_workspace/src
    vcs export --exact > ~/my_favorite_workspace_filename.txt

Run this command once per system.

    printenv > ~/my_favorite_system_environment_variables_filename.txt

This will capture the exact state of the catkin workspace, by hash not branch name, and your current environment variable settings.