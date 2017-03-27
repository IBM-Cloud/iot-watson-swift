#Overview

The previous STEPS 1-4 showed us how easily you can connect an IoT to IBM Bluemix and leverage the Watson analytics and external APIs (Twitter and Twilio). This lab demonstrates a further integration of the IoT with smart devices. This lab will show you how you can connect an iOS app with an IoT with the usage of IBM Watson IoT Platform. Optionally we will start to communicate with a robot connected to Raspberry Pi. We will add Voice User Interface to invoke commands on Raspberry Pi. And optionally Voice UI will be all for hands-free usage of the popular STEM robot – iRobot Create2.

## Prerequisites 
You need the following software/hardware:

-	finished STEPS 1-4
-	(optional) iRobot Create2

The following graph shows the architecture of this lab. On the left side on the bottom there is a smart device that connects to Watson IoT Platform service hosted on the Bluemix. Then the commands issued from the smart device invoke actions on the Raspberry Pi. Raspberry Pi is optionally connected thru a serial port with iRobot Create2.

![architecture](https://github.com/blumareks/iot-watson-swift/blob/master/lab3/img/architecture.png)


And the final Node.Red flow working with the Rapberry Pi that receives the command, and selects if it is a BEEP or DOCK:

![the flow](https://github.com/blumareks/iot-watson-swift/blob/master/lab3/img/lab3RpiFlow.png)



If you have the robot (iRobot Create2) - you might want to connect it now:

![connecting RPi to iRobot Create2's serial port](https://github.com/blumareks/iot-watson-swift/blob/master/lab3/img/connectRPi2_to_create2.png)
