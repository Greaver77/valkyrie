######The content of this page is updating frequently.

##Onboard Valkyrie Computers  

> **"640 kB ought to be enough for anybody"** - Bill Gates

> **"64 gb of ram ought to be enough for java"** - Jesper Smith  

The Valkyrie platform includes two onboard 'high level' computers. We refer to the computers collectively as the _Brainstem_. Individually the computers are referred to by class, _Link_ and _Zelda_.

The _Link_ computer is located on the robot's right side, slightly dorsal, under the right arm. The _Zelda_ computer is located on the robots left side, slightly dorsal, under the left arm.

[[images/val_processor_layout.png]]

The primary differentiator between the two computers is the _[[Synapse]]_. The _Synapse_ is the [[MLVDS]] board responsible for connecting the _Brainstem_ with the [[turbodrivers]] in the rest of the robot.

The _Link_ computer, which runs the controller, also has the realtime kernel patch installed. The _Zelda_ computer runs the vanilla Linux kernel. 

***

###Specs

* [i7-3615QE](http://ark.intel.com/products/65709) @2.3GHz
* 16GB DDR3 1600
* 240GB SSD
* [Congatec BS77 Type2 COM Express Module](http://www.congatec.com/us/products/com-express/conga-bs77.html)
* [EFK XV1 Carrier Board](http://www.ekf.de/x/xv1/xv1_e.html)
* Ubuntu 14.04 Server


####Other Resources
[Processor User Guide](http://www.congatec.com/fileadmin/user_upload/Documents/Manual/BS77_BP77m10.pdf)  
[Processor Data Sheet](http://www.congatec.com/fileadmin/user_upload/Documents/Datasheets/conga-BS77.pdf)  



Cover robonet, MLVDS, get pics, breakout board connections and what things are plugged in where