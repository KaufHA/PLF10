# KAUF Power Monitoring Smart Plug (PLF10)


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


## Configuration Entities
If using the precompiled binary or kauf-plug.yaml as a package in the ESPHome dashboard, the following configuration entities are automatically created.  Entities listed as disabled by default can be enabled in Home Assistant, or simply modified through the web interface by clicking "Visit Device" in Home Assistant or typing the plug's IP address into a web browser.

***Blue LED*** light entity - This is in the configuration section because the main intent is to control the blue LED's brightness.  However, you can also directly control the blue LED in automations or manually.

***Blue LED Config*** select entity - Configures the behavior of the blue LED.  Has the following options.  Defaults to *Power Status*.
- *Power Status*: LED follows relay state.
- *No Automation*: The plug will never automatically change the LED, but the LED can still be controlled via the light entity.
- *Invert Power Status*: LED follows the inverse of the relay's state (LED on when relay is off).
- *Error Status*: The LED will blink when an error is detected.  The most common errors are being unable to connect to Wi-Fi or Home Assistant.
- *Error and Power*: The LED will follow the relay state, but then also blink when an error is detected.
- *Error and Invert Power*: The LED will follow the inverse of the relay state, but then also blink when an error is detected.

***Red LED*** light entity - Same as the Blue LED light entity, but for the Red LED.

***Red LED Config*** select entity - Same as the Blue LED select entity, but for the Red LED.  Defaults to *Error Status*.

***Button Config*** select entity - Defines when the button toggles the relay.  To disable the button toggling the relay, select the *Don't Toggle* option.  Otherwise, you can select the relay to toggle either on press or on release of the button.  Toggle on release might be desired in order to have a different action performed when the button is held for certain amount of time.  For instance, the precompiled binary defaults to toggling on release so that the toggle can be blocked in case the button is held for 5 seconds to reenable the Wi-Fi AP.

***Debounce Time*** number entity - Defines an amount of time that the button needs to be held before toggling the relay.

***Monitoring Mode*** select entity - Disabled by default.  Modifies the frequency and mode of power monitoring sensors.  Defaults to *10s P / 40s V,I*.
- *10s P / 40s V,I* - Power is measured and reported every 10 seconds.  Current and voltage are each reported every 40 seconds, alternating such that one is reported every 20 seconds.
- *10s P,I Only* - Power and current are both reported every 10 seconds.  Voltage is never reported.
- *10s P,V Only* - Power and voltage are both reported every 10 seconds.  Current is never reported.
- *2s P,I Only* - Power and current are both reported every 2 seconds.  Voltage is never reported.
- *2s P,V Only* - Power and voltage are both reported every 2 seconds.  Current is never reported.
- *YAML Configured* - Uses the values defined by substitutions in YAML.  For the precompiled binaries, this is the same as *10s P / 40s V,I*.  See Power Monitoring Mode below for more information on customizing.

***No Hass*** switch entity - Disabled by default.  Turn this switch on if not using Home Assistant with the plug.  Prevents the plug from flashing an error due to no API connection and rebooting every 15 minutes.

***Scale Current*** number entity - Disabled by default.  Scales the current sensor.  Can be used to calibrate the plug.

***Scale Power*** number entity - Disabled by default.  Scales the power sensor.  Can be used to calibrate the plug.

***Scale Voltage*** number entity - Disabled by default.  Scales the voltage sensor.  Can be used to calibrate the plug.

***Use Threshold*** number entity - Disabled by default.  Sets a threshold for the *Device in Use* binary sensor.  The binary sensor turns on if the power detected by the plug exceeds the threshold.


## Advanced Settings
When using kauf-plug.yaml as a package in the ESPHome dashboard, you can configure the following aspects by adding substitutions.  The substitutions section of kauf-plug.yaml has comments with more explanation as well.

***friendly_name*** - The friendly name will be used to name every entity in Home Assistant.  Add a substitution to change this to something descriptive for each device.

***sub_restore_mode*** - defines the state of the relay on boot-up.  See more about the options under restore_mode here: [GPIO Switch](https://esphome.io/components/switch/gpio.html)

***disable_entities*** - Adding a substitution to redefine this to "false" will result in all entities being automatically enabled in Home Assistant.

***button actions*** - _sub_on_press_, _sub_on_release_, _sub_on_hold_5s_ can all be used to define scripts that will run based on button press/release/hold if you want something different than the default actions to happen.  A _sub_on_hold_5s_ script will execute at the 5s mark while the button is still being held.

***sub_toggle_check*** - defines a script that, if running, will stop the button from toggling on release.  Can be used to stop a button press action from occuring when a hold action executed instead.

***default_button_config*** - defines the default option for the button config select entity.

***power monitoring calibration*** - all of the values used to calibrate the power monitoring calibration can be overwritten using substitutions to make the calibration more accurate.

***power monitoring mode*** - in addition to the 5 presets in the Monitoring Mode select entity, any desired settings for the power monitoring mode can be set via substitutions.  See the change_mode_every, initial_mode, and update_interval settings on the [ESPHome HLW8012](https://esphome.io/components/sensor/hlw8012.html#configuration-variables) page.  The select entity needs to be set to "YAML Configured" for the substitutions to take effect.

## Factory Reset
Going to the plug's URL in a web browser and adding /reset will completely wipe all settings from flash memory.  Note that this will wipe the plug's memory of whether the relay was on or off, and therefore the plug may turn off.


## Troubleshooting
General troubleshooting ideas are located in the [Common repo's readme](https://github.com/KaufHA/common/blob/main/README.md) and [on our website](https://kaufha.com/troubleshooting/)

## Recommended Tasmota Template

```
{"NAME":"KAUF Plug","GPIO":[576,0,320,0,224,2720,0,0,2624,32,2656,0,0,0],"FLAG":0,"BASE":18, "CMND":"SwitchDebounce 100"}
```

## Links
- [Purchase plugs on Amazon](https://www.amazon.com/dp/B09JQ3LRHB)
- [KAUF YouTube Channel](https://www.youtube.com/channel/UCjgziIA-lXmcqcMIm8HDnYg)
- [KaufHA Website](https://kaufha.com/plf10)
