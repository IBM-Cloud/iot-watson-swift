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

### Step 1. 
Create the Internet of Things Platform Starter in IBM Bluemix and connect to a virtual sensor:
Deploy deploy the Internet of Things Platform Starter, which is a boilerplate application, and connect it to a virtual sensor on a web page. You don't need your Raspberry Pi device for this section.
Log in to Bluemix and click Catalog > Boilerplates > Internet of Things Platform Starter. 
Enter a name and host for your application. Both names must be unique. Then, click Create.

After the application launches, click View App and then on go to your Node-RED flow editor.

You should see Flow 1 running on Bluemix with a virtual thermometer. (Ignore the top flow above the flow for now)


After you start your Internet of Things Platform Starter instance, click the following link to connect a temperature simulator to the IBM IoT app In node as shown in blue in Flow 1: [ibm.biz/iotsensor](http://ibm.biz/iotsensor).  

Copy the value in the upper-right corner of the virtual thermometer. In the flow editor, double-click the IBM IoT App In node. 

Paste the ID into Device Id field. Click Done and then deploy the flow.

Go to the virtual sensor and increase the temperature to 41° C or more. 
In the flow editor, note that the flow has three green output debug nodes that show flow data in the debug pane. 
Disconnect the top green Debug output payload node in the top flow by clicking the connecting line and pressing Delete on your keyboard. Disconnect the device data node on the bottom flow as shown in the following image. Then, click Deploy.
You might need to scroll down in the debug pane to see the simplified view of temperatures.

### Step 2. 
Prepare the Raspberry Pi to use as an input source
Be sure you already set up your Raspberry Pi device. For help with setting up the device, see the Help videos and the Raspberry Pi Software Guide.
Turn on the Raspberry Pi device with the Raspbian Jessie. 
Connect all the peripherals: monitor, keyboard, mouse, and a mini USB smartphone or digital camera charger for power.
Configure the device network to use the same LAN that you are using. Suggestion: Use an access point that you might reuse in different locations.
Set up networking and launch the Node-RED service. When you launch a terminal, get the IP address that is assigned to your Raspberry Pi by running this command: ifconfig
Read and save the assigned IP address. In typical LAN locations, it is something like 192.168.1.213.
When the IP address is known and if your computer is on the same LAN network, you are ready to launch a terminal on your computer.
Run the following Secure Shell (SSH) command and enter the assigned IP address in place of the example IP address: ssh pi@192.168.1.213
If the command is unknown or you have problems with SSH, see Configuring SSH.
When you see the prompt for the password, enter ```raspberry``` and press Enter. (This is the standard password.)

Start Node-RED. You can start it automatically or manually.
Enter this command to automatically start Node-RED: 
```sudo systemctl enable nodered.service```
Enter this command to manually start Node-RED: 
```node-red-start```

Enter ifconfig to see the IP address of the Raspberry Pi device.
Enter the IP address in a browser. You can see the empty Node-RED environment running on the Raspberry Pi.


### Step 3. 
Connect the Raspberry Pi Node-RED flows to IBM Bluemix
Load a new Node-RED flow into the flow editor on the Raspberry Pi device:
Copy the raw JSON from this web page to your clipboard: https://raw.githubusercontent.com/ibm-messaging/iot-device-samples/master/node-red/device-sample/quickstart.json.
In the flow editor, create a new flow tab. Then, import the new flow: click the Menu icon > Import > Clipboard. 
Double-click the red Exec node (getCPUtemp) that retrieves the CPU temperature from the Raspberry Pi device. Add the following information:
Command: vcgencmd
Under Append: measure_temp
Name: GetCPUtemp

Click OK.

Connect the Node-RED flow on the Raspberry Pi with the Node-RED flow that you already have on Bluemix. The communication between the Node-RED instance running on the Raspberry Pi and the one running on Bluemix is provided by IBM Watson IoT Platform/Quickstart, which is based on MQTT, a lightweight messaging protocol.


Double-click the blue Watson IoT Output node (wiotp out) in the flow on the Raspberry Pi device. Select Quickstart and enter a unique value for the Quickstart Id. This value can be any string, but it must be unique in the entire system. Click OK.

Double-click the blue IBM IoT App In node and enter the same Device Id that you used for the one on the Raspberry Pi. This is how the two Node-RED environments will communicate. Click Done.


Click the Timestamp node on the Raspberry Pi to start the flow that will send CPU data to the Node-RED instance on Bluemix every 5 seconds.

Review the output in the debug panes. 
The two outputs are dissimilar because the Node-RED flow on the Raspberry Pi does not have the trigger warning that you used for the Node-RED flow in Bluemix. 
If you disconnect the connections to the green debug node on the Raspberry Pi, you won't see any output in the first debug pane, which is highlighted in red, but you will see output in the debug pane highlighted in blue in the following image: 

Step 4. Add social service notifications to your flow
You can easily add other services on Node-RED on Bluemix, such as Twitter, a Cloudant database, or a language translator service. In this step, you'll add social service notifications through Twitter.
Under social, drag a twitter out node onto the canvas under the cpu status node so that you can notify others when the CPU temperature exceeds 40° Celsius.


Click the connecting port of the danger node on the right and connect it to the Tweet (twitter out) node.


Double-click the Tweet node to edit its information.


Click the pencil icon to edit and associate the Twitter node with the Twitter account of your choice.
Click Done and then deploy the Node-RED flow. 
Whenever the temperature exceeds 40° Celsius, a tweet is generated. Note that duplicate tweets are filtered by Twitter. Now your followers can let you know that something is wrong with the temperature in your greenhouse.

The next step will be to save the temperatures in a Cloudant database by adding a Cloudant database insert node to the flow. These steps are described in the next lab.
Experiment with your flow by adding other nodes.   



Let’s configure the timestamp node to add the time to the temperature in the msg.payload to insert it in the Cloudant DB.
```js
msg.timestamp= new Date().toISOString();
return msg;
```
Optionally you might want to change it further for the readability purposes. When you are ready to deploy the changes – please re-Deploy the Node.Red flow.
Let’s see how the temperatures are being recorded. We can open the Cloudant DB Dashboard and investigate the temperature records.
