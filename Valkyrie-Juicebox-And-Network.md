# Overview  
The Juicebox is a a power distribution half server Pelican case. The contents of the case include two lambda power supplies, a QNAP NAS, and a Nighthawk wireless router. 

## Layout  
America Juicebox  
[[images/JuiceboxUS.png]]  

European Juicebox  
[[images/JuiceboxUK.png]]  

## Juicebox Network  
Each Juicebox is designed to be a self contained robot network. The supplied Travel NAS runs an IHMC Logger as well as serves as a mount point for the Visualizer computer's SMT logs. The Nighthawk handles routing as well as NAT to the outside world. Additionally the Nighthawk serves DHCP addresses above 10.185.0.200.  

**Val:**  
 * Link Processor: ```10.185.0.(10, 20, 30, 40)```  
 * Zelda Processor: ```10.185.0.(11, 21, 31, 41)```  

**Visualizer Computer:** ```10.185.0.(101, 102, 103, 104)```  
**Travel Logger NAS:** ```10.185.0.5```  
**Nighthawk Router:** ```10.185.0.1```  

<img src="https://github.com/NASA-JSC-Robotics/valkyrie/wiki/images/ValNetwork.png" width="650">  