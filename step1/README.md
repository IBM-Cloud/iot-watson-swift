## Overview
Let’s say we are monitoring the temperature of a green house. We want to learn if the temperature exceeds 40 degrees Celsius to alert the manager and / or social networks to support administration of the equipment. 
This lab will show how you can deliver this type of functionality with the popular IoT device Raspberry Pi with its great price/feature parameters.
This lab shows you how to create the connection between the Internet of Things (IoT) device and the IBM Bluemix cloud. You are going to use Raspberry Pi to push information from its temperature sensor (the temperature of the CPU) to the cloud. In addition you are going to publish the information to Twitter about the state of your device.
To create the application in this lab, follow these main steps:

1.	Use the Bluemix to create the Internet of Things platform starter.
2.	Connect to the simulated device.
3.	(optional) connect to the real device.
4.	Publish information to the Twitter.

Here come the flows showing processing of the information from Raspberry Pi to Bluemix Node.Red.

![flows Raspberry Pi -> Bluemix/WatsonIOT platform](img/flows.lab1.png)

## Prerequisites 
You need the following software:

-	IBM Bluemix account http://bluemix.net
-	a Twitter account

## Adding the "temperatures" db and Swift iOS app
In addition to Twitter you can easily add a Cloudant database node to insert the temperatures into database, and then you might want to read them from your smart device, when you want to validate what is happening with your physical temperature sensor (and follow up with your social network followers from the previous Step 4).
Let’s first add the Cloudant database called “temperatures” to the existing Node.Red internal Cloudant DB – from the dashboard just select Databases and hit Create Database 

then in the Node.Red flow add Cloudant insert node,  configure it to insert data into the internal Cloudant DB with all the msg parameters

and connect the Cloudant node and function nodes to the previously created Node.Red flow at the output of the temp node as shown:

![flows Raspberry Pi -> Bluemix/WatsonIOT -> Cloudant DB](img/flows.lab1.cloudant.png)

Let’s configure the timestamp node to add the time to the temperature in the msg.payload to insert it in the Cloudant DB.
```js
msg.timestamp= new Date().toISOString();
return msg;
```
Optionally you might want to change it further for the readability purposes. When you are ready to deploy the changes – please re-Deploy the Node.Red flow.
Let’s see how the temperatures are being recorded. We can open the Cloudant DB Dashboard and investigate the temperature records.
