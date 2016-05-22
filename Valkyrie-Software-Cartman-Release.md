# Valkyrie Software Cartman Release  

<p align="center">[[images/cartman.png]]</p>  

## Overview  
Words here about what this release contains in terms of features

## How to Install  
The JSC team is pleased to announce the latest release of Valkyrie Core Software. The steps below will outline a path to upgrade.

#### Steps
##### Step 1  
Download the appropriate system configuration package from the selections below.  
  - Robot IO Computer  
  - [Link 02 MIT](https://drive.google.com/file/d/0B4Esozi1aH0sUHVCVDZiU1lkVEk/view?usp=sharing)  
  - [Link 03 NEU](https://drive.google.com/file/d/0B4Esozi1aH0sYTlKTW9UTzJ5cnc/view?usp=sharing)  
  - [Link 04 UoE](https://drive.google.com/file/d/0B4Esozi1aH0sYWZnM3Z4b25qZXM/view?usp=sharing)  
  - Robot Vision Computer  
  - [Zelda 02 MIT](https://drive.google.com/file/d/0B4Esozi1aH0sd0V1RXNKMGtxZUE/view?usp=sharing)  
  - [Zelda 03 NEU](https://drive.google.com/file/d/0B4Esozi1aH0sZVY5UjZTekxlN1U/view?usp=sharing)  
  - [Zelda 04 UoE](https://drive.google.com/file/d/0B4Esozi1aH0sN0VGcFRpSmMtWjA/view?usp=sharing)  
  - Valkyrie Visualizer Computer  
  - [Vis 02 MIT](https://drive.google.com/file/d/0B4Esozi1aH0sTW9LNDFPbTNkM2c/view?usp=sharing)  
  - [Vis 03 NEU](https://drive.google.com/file/d/0B4Esozi1aH0sOHRaNndjVGhNVHM/view?usp=sharing)  
  - [Vis 04 UoE](https://drive.google.com/file/d/0B4Esozi1aH0sWF9lQVY0cGRldFk/view?usp=sharing)  
  - Testbed Computer or Generic Developer  
  - [Generic System Config](https://drive.google.com/file/d/0B4Esozi1aH0sei1kT01MQ2dMbWc/view?usp=sharing)  

##### Step 2  
Remove the existing system configuration package. Please note, the new package must be downloaded first.  
**NOTE** Backup your current networking settings. Installation of the new system config package will overwrite modifications made to /etc/network/interfaces and /etc/hosts.  

```sudo apt-get remove nasa-val-system-config*```  

##### Step 3  
Install the downloaded system configuration package.  

```sudo dpkg -i nasa-val-system-config*.deb```  

##### Step 4  
Remove your existing workspace. 

```rm -rf ~/val_indigo/*```

##### Step 5  

Install a fresh workspace.  
[Checking out Valkyrie source code](Valkyrie-Source-Code)  


## Listing of hashes for each repo

Project | Hash | Version 
:--------:|:--------:|:--------:
nasa_common_cmake | b71e0eebb79f55a1b2b8ad1457a78f2d1064a73f | 2.0.0
nasa_common_logging | cafea71842e1e7a515d503036f2a770ab741802c | 3.0.0
nasa_indigo_workspace | 60cfc08a46310e0f4fe6a99b75591169b37f51fd | 1.0.0  
nasa_pyqtlib | 52df7a127ab636350c4e7f88973dfc8fe26eca1b | 2.0.0
ui_builder | 8dd5e90fd589a2ddda545354676119e0ad307c14 | 2.0.0
imu_3dm_gx4_15 | dba8e0b60a4d53b730e817d9777796038fd68afc | 2.0.0
rtmidi | dd4b28315a4dd7d6196c6fdc2d88b8412e54c1c6 | 3.0.0
rttlua_completion | 66294e1e70a002eab0f4a6dd0900dc608095833a | 2.0.0
shared_memory_transport | 54ced609f1cc3a97a846deaf0047ffa9655476a7 | 2.0.0
shared_memory_transport_interface | 622a94549b6b5b132c7c488add7c1ac9fdc53a1e | 2.0.0
shared_memory_transport_qt | 88d1f21ae8d9066d1703167e8dd85d659b397b48 | 2.0.0
shared_memory_transport_sliderboard | 1d73588929feb3b2fbbe5af728197c351dc688c2 | 3.0.0
nasa_val_common | 4883746a2a6a628a6e0e56ea7e317d7ca235e9c4 | 2.0.0
athena_api | 4e890e74731ab856c5823d1821982cfc98371d1d | 3.0.0
athena_hdlrsmp | 9f6d5b4e812c7d07d69c3cdb3f458e9a1db7baa5 | 1.0.0
nasa_val_config | 801f02422118952c61edd2f426593ca6524bd977 | 2.0.0
nasa_val_embedded_utils | 652e392da2a04de97741070b2539fce1f142d04e | 3.0.0
nasa_val_system_config | 39e7fb8358dd9c2b360b1920a123365a8f288244 | 3.0.0
power_api | d1571ef534e4cd1877035079ddab77845084b911 | 3.0.0
robonet_stream_message_protocol | f68f0cd3fb7c2f063c74052be22c871880b868b6 | 2.0.0
robonet_synapse_driver | c2f9123406001d652bbb44ac8e59ced480774e03 | 2.0.0
robonet_tools | 293279c4af125de01a892212720ae45f4f80d3e4 | 3.0.0
turbodriver_api | 9e60bbad54439f85f4e3dd1e7c5d09c78fc94b50 | 2.0.0
val_control | 81e3166a13c637d5bf869a41c433d45838ac8614 | 3.0.0
val_controllers | a0759788621b2ef7d99adf98ef963ed1341bdf3e | 2.0.0
val_deploy | 483ef22ee353b7ca3665146cfb74869892f2263a | 3.0.0
val_description | 280cefa685103b757ca22e883fc0f33cd62db2ad | 3.0.0
val_gazebo | 1a3b442e4fdddf1981c7eed48b87aad437514051 | 2.0.0
val_sensor_interfaces | 696355cd7753348c755d5a9510041adedaac9019 | 2.0.0
val_msgs | ccdb5c7893aefe01268fe29bfb3637b9cdb2fdfe | 2.0.0
val_vanguard_config | ba1c323d9f3ec599b5efaa1a633ef10ad321f757 | 1.1.0
val_user_interfaces | 4728fb07b5a8421593a2d57d732bb3ca07a182f6 | 2.0.0
vanguard | 4c17968f8b6a352daea36c0651fb9004605c0285 | 1.2.0


## Help/Troubleshooting
Thanks for sticking with us through our first public Master release. If you find a problem please send in an issue here: [[Find a bug?|https://github.com/NASA-JSC-Robotics/valkyrie/issues]]  

If you need direct help, feel free to [[Contact Us|Contact-Us]]  