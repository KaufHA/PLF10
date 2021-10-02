# PLF10
Files for the PLF10 Power Monitoring Smart Plug

* **kauf-plug.yaml** is the yaml file recommended as a template for importing into a user's ESPHome dashboard. You will maintain all the functionality of the stock plug except for the Wi-Fi access point will be disabled. _Note that you must enter your local wifi credentials into this yaml file._
* **kauf-plug-lite.yaml** is a pared down version of kauf-plug.yaml that removes some functionality and just leaves the bare minimum for the plug to operate as a power monitoring plug in Home Assistant. _Note that you must enter your local wifi credentials into this yaml file._
* **kauf-plug-upgrade.yaml** is the yaml file used to generate the upgrade bin file.  Probably not worth bothering with for end users, and may not compile without using our forked ESPHome source code.
* **kauf-plug-factory.yaml** is the yaml file used to generate the manufacturer-flashed firmware.  May have extra functionality that is pointless for home users.  _Do not bother trying to use this file._

Tasmota template:
{"NAME":"Kauf Plug","GPIO":[320,0,576,0,224,2720,0,0,2624,32,2656,0,0,0],"FLAG":0,"BASE":45}
