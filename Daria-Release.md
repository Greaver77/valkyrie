# Valkyrie Software Daria Release  

<p align="center">[[images/Daria_release_image.png]]</p>  

## Release Date
~July 1st 2016

## Release Overview,Proposed Features, and Updates
The main focus for this release is centered around getting a better handle on our embedded code repositories as well as improving our firmware loader. The benefits of these being,

- Making it easier to iterate on and create future releases of embedded software
- Setup our firmware loader so that binaries from embedded code updates can be downloaded and deployed to turbodrivers in remote locations automatically.

Other features that will be added in this release include,

- Better handling of IMU error packets. The bad packets will still occur, but we now properly handle the bad packets and the cleanly shut down the controller manager. This will no longer cause ui_builder to freeze. 
- The Force/Torque sensors are correctly in the URDF as a fixed joint as is done with the IMU's and cameras.
- Official switch to [Gazebo 7](http://gazebosim.org/#collapseVersion7_1). Since Gazebo 4 is EOL, we have been working with the folks at OSRF to switch to Gazebo 7 and expect to be ready to officially abandon Gazebo 4. 

