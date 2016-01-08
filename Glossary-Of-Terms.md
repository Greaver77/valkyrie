**COM Express** - Computer-On-Module (COM) is a highly integrated and compact PC form factor.  This is the form factor of the main computers used on Valkyrie.  For more information, [Computer-on-module](https://en.wikipedia.org/wiki/Computer-on-module) entry on Wikipedia  

**ER/ER4** - ER is the designated code for the Software, Robotics, and Simulation Division at NASA's Johnson Space Center.  ER4 is the code used for the Robotics Systems Technology Branch within the division.  

**Forearm Mass Sim**

**HAPI** - Hardware API  

**JSC** - [Johnson Space Center](http://www.nasa.gov/centers/johnson/home/index.html)

**Juice Box** - This is our term for the box that holds the power sources. It also holds a network attached storage(NAS) device for storing log files as well as a wireless router.  
<img src="https://github.com/NASA-JSC-Robotics/valkyrie/wiki/images/JuiceBox.png" width="250">  

**Link** - The real-time computer. It is located on the robots right side.

<img src="https://github.com/NASA-JSC-Robotics/valkyrie/wiki/images/Link.png" width="250">

**Mass Sim** - The Valkyrie robot platform was designed from the start with battery use in mind. The Mass Sim approximates the weight of a full battery, and offers some capacitance. The capacitance in the Mass Sim protects the robot from back EMF.  

**MLVDS** - Multi-drop Low-voltage Differential Signal.  MLVDS is a physical-layer electrical specification.  MLVDS is the physical layer used by [Robonet](Robonet)  

**Primary** - The primary is the structure of the upper torso. The Primary houses a simple distribution board that connects each of the robots limbs to the Secondary.  

**Robonet** - Robonet is the field bus that connects the main computers to the embedded controllers.  See [here](Robonet) for more information.

**Secondary** - The Secondary is the removable core structure in the upper torso that consists of the PDBMTI, Link, Zelda and various Turbodrivers.  

**SMT** - [Shared Memory Transport](Shared-Memory-Transport).  A mechanism used for inter-process communication.  Valkyrie's primary usage is to expose low-level hardware data to the control system using SMT.

**Turbodriver** - A Turbodriver is a single-axis embedded motor controller module developed at JSC. These are the motor controllers used to control most of the actuators on Valkyrie. These modules are distributed throughout the robot, generally near the motor for which a module controls. They are not very visible with the covers on.  Turbodrivers communicate to the main I/O computer (Link) over [Robonet](Robonet).  Data from the Turbodrivers are exposed to the rest of the system using [SMT](Shared-Memory-Transport)

<img src="https://github.com/NASA-JSC-Robotics/valkyrie/wiki/images/Turbodriver.png" width="250">  

**Vanguard** - Vanguard is a software suite used to empower operators to interact with remote systems (like robots) in a safe, managed way, over communication channels that would normally allow unsafe commanding.  Tasks ranging from editing files, to installing software, to starting and stopping the processes are accomplished through a well-defined communication interface.  Vanguard implements the Majordomo Protocol(https://github.com/zeromq/majordomo) with a collection of task-specific workers and accompanying clients.  The deployment of Vanguard components is flexible and can be custom tailored to meet the needs of simple "remote execution" systems as well as human-rated safety critical systems.

**Zelda**-The non real-time computer. Zelda is located on the robots left.

<img src="https://github.com/NASA-JSC-Robotics/valkyrie/wiki/images/Zelda.png" width="250">
