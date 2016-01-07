[[images/valkyrie-robot-nasa.png]]  

# Ring LED Legend

Two concentric rings of LED lights are mounted in the center of Valkyrie's chest. Their color and actions are used to convey the status of the robot to the operator.   

###### Ring LED :
Color | Action | Description | Picture
:--------:|:--------:|:--------|:------------------------------------------
Rainbow | Rotating | Robot is booting up. Only the computers, router, and Estop are powered. Motor power may not be turned on until the bootup sequence is completed | <img src="https://github.com/NASA-JSC-Robotics/valkyrie/wiki/images/Ring_LED/rainbow.gif" width="500"> 
Red | Rotating | Robot is up but does not have communication with the computer | [[images/Ring_LED/no_comm.gif]]  
White | Rotating | Robot has communication and is ready to turn on logic and motor power | [[images/Ring_LED/idle.gif]]  
Green | Rotating | Logic power is on, motor power is off | [[images/Ring_LED/logic_power.gif]]  
Purple | Rotating | Logic power is on, motor power is in the process of turning on | [[images/Ring_LED/purple.gif]]
Royal Blue | Rotating | Logic power is on, motor power is on and running from tether | [[images/Ring_LED/royal_blue.gif]]
Light Blue | Rotating | Logic power is on, motor power is on and running from battery | [[images/Ring_LED/light_blue.gif]]
Orange | Rotating | Estopped; something has made the robot turn off motor power | [[images/Ring_LED/orange.gif]]
