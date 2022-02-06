# PLF10


The recommended way to import a plug into your ESPHome dashboard is through the dashboard import feature. The plug will need to be updated to 1.83 or greater to be discovered by the ESPHome dashboard. You can accomplish the same thing without updating first by using the following yaml modified as desired.

The friendly_name substitution is recommended and will not be automatically created by the ESPHome dashboard import.

```
substitutions:
  name: bedroom-lamp
  friendly_name: Bedroom Lamp
  
packages:
  kauf.plf10: github://KaufHA/PLF10/kauf-plug.yaml

esphome:
  name_add_mac_suffix: false

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

This repo contains files for the PLF10 Power Monitoring Smart Plug.

***components* directory** - Custom components needed to compile the PLF10 Smart Plug firmware. These don't need to be downloaded, the yaml files automatically grab them by reference to this github repo. Every subfolder not starting with kauf_* is copied from stock ESPHome and edited for our products.

***config-update* directory** - Files needed in the ESPHome config directory to compile the update bin file for the smart plugs.

***config-factory* directory** - Files needed in the ESPHome config directory to compile the factory bin file for the smart plugs.

***kauf-plug.yaml*** - config yaml file needed to import a plug into your ESPHome dashboard and keep all custom KAUF functionality.

***kauf-plug-lite.yaml*** - config yaml file needed to import a plug into your ESPHome dashboard with only basic power monitoring smart plug functionality.
