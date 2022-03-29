# PLF10


The recommended way to import a plug into your ESPHome dashboard is through the dashboard import feature. The plug will need to be updated to 1.83 or greater to be discovered by the ESPHome dashboard. You can accomplish the same thing without updating first by using the following yaml modified as desired.

The friendly_name substitution is recommended and will not be automatically created by the ESPHome dashboard import.

```
substitutions:
  name: bedroom-lamp
  friendly_name: Bedroom Lamp

packages:
  kauf.plf10: github://KaufHA/PLF10/kauf-plug.yaml

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

## Repo Contents

This repo contains files for the PLF10 Power Monitoring Smart Plug.

***kauf-plug.yaml*** - The yaml file recommended to import a plug into your ESPHome dashboard and keep all custom KAUF functionality.  This is the yaml file incorporated automatically when the dashboard import feature is used.

***kauf-plug-lite.yaml*** - A yaml file without any Kauf custom components but otherwise keeping as much functionality from kauf-plug.yaml as possible.

***kauf-plug-minimal.yaml*** - A yaml file to import a plug into your ESPHome dashboard with only basic power monitoring smart plug functionality.

***kauf-plug-update.yaml*** - The yaml file to build the update bin file.  Generally not useful to end users.

***kauf-plug-factory.yaml*** - The yaml file to build the factory bin file.  Generally not useful to end users.


## Advanced Settings
When using kauf-bulb.yaml as a package in the ESPHome dashboard, you can configure the following aspects by adding substitutions.  The substitutions section of kauf-bulb.yaml has comments with more explanation as well.

***friendly_name*** - The friendly name will be used to name every entity in Home Assistant.  Add a substitution to change this to something descriptive for each device.

***sub_restore_mode*** - defines the state of the relay on boot-up.  See more about the options under restore_mode here: [GPIO Switch](https://esphome.io/components/switch/gpio.html)

***disable_entities*** - Adding a substitution to redefine this to "false" will result in all entities being automatically enabled in Home Assistant.

***button actions*** - _sub_on_press_, _sub_on_release_, _sub_on_release_quick_, and _sub_on_release_short_ can all be used to define scripts that will run based on button press/release/hold if you want something different than the default actions to happen.

***power monitoring calibration*** - all of the values used to calibrate the power monitoring calibration can be overwritten using substitutions to make the calibration more accurate.

## Factory Reset
Going to the plug's URL in a web browser and adding /reset will completely wipe all settings from flash memory.


## Troubleshooting
Any build errors can usually be resolved by upgrading the ESPHome dashboard to the latest version.  On the days when ESPHome updates are released, it may take us up to 24 hours to make necessary changes to our custom components during which time you may see build errors.  Please be patient.  
  
If you are still getting errors after upgrading the ESPHome dashboard to the latest version, try deleting the .esphome/packages and .esphome/external_components subfolders from within the ESPHome config directory.



## Recommended Tasmota Template

```
{"NAME":"KAUF Plug","GPIO":[576,0,320,0,224,2720,0,0,2624,32,2656,0,0,0],"FLAG":0,"BASE":18}
```

## Links
- [Purchase plugs on Amazon](https://www.amazon.com/dp/B09JQ3LRHB) (*Temporarily out of stock*)
- [KAUF YouTube Channel](https://www.youtube.com/channel/UCjgziIA-lXmcqcMIm8HDnYg)
