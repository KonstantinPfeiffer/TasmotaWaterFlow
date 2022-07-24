

Use https://benzino77-tasmocompiler-5dvopnzodev.ws-eu54.gitpod.io/


to compile a Tasmota Version with "Script" instead of "Rules" for your Platform.

Define the follwing declares:


`
#define USE_SCRIPT_TIMER  
#define USE_SCRIPT_WEB_DISPLAY  
#define USE_SCRIPT_JSON_EXPORT  
#define USE_BUTTON_EVENT  
#define USE_SCRIPT_SUB_COMMAND  
#define USE_SCRIPT_GLOBVARS  
#define USE_GOOGLE_CHARTS  
#define USE_SCRIPT  
#define USE_BUTTON_EVENT  
`


Flash the Binary to your ESP. 
You can use: 
https://github.com/tasmota/tasmotizer for ESP8266 to directly upload the image 

for ESP32 you can use your upload tool of your choice, or most easy way if you do not have anything set up yet:

Use https://tasmota.github.io/install/ to intasll the default ESP32 Tasmota image, then use the "Upgrade Firmware" function to upload the custom image.

When you are connected, copy the follwing Script to the Script Console, don´t forget to activate. You also have to configure MQTT. The Values from Counter1 are taken, so you have to configure your Profile to "Generic" and define the Counter on the GPIO you connected the WaterFlow Meter.



