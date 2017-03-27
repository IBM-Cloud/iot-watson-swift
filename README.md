# iot-watson-swift
If you like this project - give it a star!

This project covers Watson services (Visual Recognition, Speech to Text, Text to Speech),  Swift for iOS, Node.Red on Raspberry Pi, and on Bluemix, Cloudant NoSQL DB, MQTT protocol over Watson IoT Platform. It is good for beginners - I will show how to build everything from scratch. And if I use tools, I will explain why I need a hammer to nail the boards :-)

Shall you want to get your home robot (or simply Raspberry Pi - **called RPi** ) connected and augmented with Watson services, and controlled by a mobile app written in modern Swift language to manage your device and answer questions on the weather and golf? If the answer is yes - this is this project is for you.

## STEP 1. 
In this project first you need to connect RPi to Bluemix (over internet). Bluemix is the IBM Cloud - there are essential Watson and *common* services that we are going to leverage in our project. Add Twitter node for Social Network communications. Then you need to publish some data to Cloudant NoSQL DB.

## STEP 2. 
Read the data from an iOS device in a Swift App.

## STEP 3.
Furthermore you can add 2-way communications from Bluemix to RPi - to invoke picture grabbing (and if you happan to have the Raspcam - a RPi camera - we will use it to take a picture), and then I will send the picture from RPi to Bluemix (I will store the image in the DB).

## STEP 4.
I will add the first Watson Service - the Visual Recognition - to our service to analyze picture. I will add a button and function to the iOS app to show the picture if the button "show the picture" is pressed.

## STEP 5.
Finally I will connect the iRobot Create2 robot (based on iRobot Roomba 600 series) over the Serial-USB cable to RPi.

## STEP 6.
I will invoke some commands from the iOS Swift app over MQTT.

## STEP 7.
Just to make things cooler - I will ask our system about the weather forecast - if it is nice - I will get the information on golf conditions.

So this simple 7 steps would allow us to augment a home appliance with Watson, and obtain a new Voice UI to create great User Experience (called as UX by many).
