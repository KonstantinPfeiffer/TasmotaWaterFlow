

Use https://benzino77-tasmocompiler-5dvopnzodev.ws-eu54.gitpod.io/


to compile a Tasmota Version with "Script" instead of "Rules" for your Platform.

Define the  declares from FlowMeter.txt


Flash the Binary to your ESP. 
You can use: 
https://github.com/tasmota/tasmotizer for ESP8266 to directly upload the image 

for ESP32 you can use your upload tool of your choice, or most easy way if you do not have anything set up yet:

Use https://tasmota.github.io/install/ to intasll the default ESP32 Tasmota image, then use the "Upgrade Firmware" function to upload the custom image.

When you are connected, copy the follwing Script to the Script Console, don´t forget to activate. You also have to configure MQTT. The Values from Counter1 are taken, so you have to configure your Profile to "Generic" and define the Counter on the GPIO you connected the WaterFlow Meter.

Save and activate the Content from FlowMeter_Final_script.txt in the Console-->Script (Not BERRY Script in ESP32!) 


