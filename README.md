# control4-2way-web-driver

This driver allows you to get and set the state of any control4 device by making
an http request. The response is in JSON format.

Use Case:
---------
I am using this (along with my homebridge-c4-plugin) to connect homekit to my
control4. So I can say "Siri turn on Kitchen Lights" or "Siri is my garage door
closed". You can use this with any other hub which supports making http requests.

Examples:
----------
- Get the current level of dimmer light:
http://CONTROLLER_IP:9000/?command=get&proxyID=25&variableID=1001

Result: {"1001":"75"}
which means the dimmer light with proxyID 25 is currently at 75%

- Update the current level of dimmer light:
http://CONTROLLER_IP:9000/?command=set&proxyID=25&variableID=1001&newValue=100

Result: {"success":"true"}

- Get the current temperature set for thermostat:
http://CONTROLLER_IP:9000/?command=get&proxyID=34&variableID=1132,1130

Result: {"1132":"68","1130":"67","success":"true"}
which means the thermostat is set to 68F and current temperature is 67F

- Update the temperature of thermostat:
http://CONTROLLER_IP:9000/?command=set&proxyID=34&variableID=1132&newValue=66

Result: {"success":"true"}

- Get list of all variables for a device:
http://CONTROLLER_IP:9000/?command=getvariables&proxyID=25

Result: {"1005":"MAX_ON_LEVEL","1006":"MIN_ON_LEVEL","1003":"CLICK_RAMP_RATE_DOWN","1007":"START_ON_LEVEL","1000":"LIGHT_STATE","1004":"PRESET_LEVEL","1008":"START_ON_TIME_MS","1001":"LIGHT_LEVEL","1002":"CLICK_RAMP_RATE_UP","success":"true"}

How to use:
------------
Sorry this is not currently easy to use :(. You will have to find the variableID
and proxyID for each device you want to connect. I hope in future we can
make it use device names and variable names instead of IDs.

- You need to either have access to ComposerPro or ask your dealer to install it
for you.
- To find proxyID, mouse over the device or check info for the device.
- To find variableID, execute:
for k,v in pairs(C4:GetDeviceVariables(34)) do print(k, v.name, v.value) end
which will print all variables, their IDs and current values.

Warning:
---------
This is completely unencrypted and unsecure. Anybody with access to your wifi
will be able to control any of your control4 connected devices. So don't open
it to internet and also make sure you have a secured wifi.
