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





## Recommended Tasmota Template

```
{"NAME":"KAUF Plug","GPIO":[576,0,320,0,224,2720,0,0,2624,32,2656,0,0,0],"FLAG":0,"BASE":18}
```
