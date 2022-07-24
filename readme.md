

Use https://benzino77-tasmocompiler-5dvopnzodev.ws-eu54.gitpod.io/


to compile a Tasmota Version with "Script" instead of "Rules" for your Platform.

Define the follwing declares:

---------COPY EVERYTHING UNDER THIS LINE---------

#define USE_SCRIPT_TIMER
#define USE_SCRIPT_WEB_DISPLAY
#define USE_SCRIPT_JSON_EXPORT
#define USE_BUTTON_EVENT
#define USE_SCRIPT_SUB_COMMAND
#define USE_SCRIPT_GLOBVARS
#define USE_GOOGLE_CHARTS
#define USE_SCRIPT
#define USE_BUTTON_EVENT

---------COPY EVERYTHING ABOVE THIS LINE---------

Flash the Binary to your ESP. 
You can use: 
https://github.com/tasmota/tasmotizer for ESP8266 to directly upload the image 

for ESP32 you can use your upload tool of your choice, or most easy way if you do not have anything set up yet:

Use https://tasmota.github.io/install/ to intasll the default ESP32 Tasmota image, then use the "Upgrade Firmware" function to upload the custom image.

When you are connected, copy the follwing Script to the Script Console, don´t forget to activate. You also have to configure MQTT. The Values from Counter1 are taken, so you have to configure your Profile to "Generic" and define the Counter on the GPIO you connected the WaterFlow Meter.


---------COPY EVERYTHING UNDER THIS LINE---------
>D
p:total=0
p:liter=0
p:highflow=0
p:midflow=420
p:lowflow=390
p:highflowTC=150
p:midflowTC=80
p:lowflowTC=30
resetb=0
delta=0
flow=0
tmp=0
cflow="none"
>B
total=pc[1]
ts1(1000)

>ti1
if resetb==1
then
resetb=0
total=0
liter=0
=>Counter1 0 
endif

delta=pc[1]-total
total=pc[1]

if delta>highflowTC 
then
cflow="high"
tmp=(delta/highflow)
endif

if delta>midflowTC
and delta<highflowTC
then
cflow="mid"
tmp=(delta/midflow)
endif

if delta<midflowTC
then
cflow="low"
tmp=(delta/lowflow)
endif

if delta==0
then
cflow="none"
tmp=0
endif


liter=(liter+tmp)
flow=tmp*60
print total:%total% delta:%delta% liter:%liter% flowrate:%flow%
svars
ts1(1000)
=>publish stat/%topic%/Flow{"FlowRate":%flow%,"PulseRate":%delta%,"WaterFlow":"%cflow%","Total":%liter%, "Counter": %total% }

>W

Total{m}%liter% Liter
FlowRate{m}%flow% Liter/min
PulseRate{m}%delta% Pulse/sec
WaterFlow{m}%cflow% 

nm(0 1000 1 highflow "Pulses per liter High" 80) 
nm(0 1000 1 midflow "Pulses per liter Mid" 80)  
nm(0 1000 1 lowflow "Pulses per liter Low" 80 )

nm(0 400 1 highflowTC "HighFlow Pulse/Sec" 80) 
nm(0 400 1 midflowTC "MidFlow Pulse/Sec" 80)  
nm(0 400 1 lowflowTC "LowFlow Pulse/Sec" 80 )

bu(resetb "Resetting" "Reset Total")
---------COPY EVERYTHING ABOVE THIS LINE---------
