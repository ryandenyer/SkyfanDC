# SkyFanDC ESPHome Package

ESPHome package for Ventair SkyFan DC ceiling fans using the Egglec SkyFanDC ESP8266 replacement module.

This repository is based on the original work by **James Eggleston (@jeggleston1981)** and extends the project with reusable ESPHome packages, simplified device configuration, configurable datapoints, fan model support, diagnostic sensors, and GitHub package distribution.

## Credits

Original project:

- James Eggleston
- https://github.com/jeggleston1981/skyfandc
- https://www.egglec.com.au

This repository builds upon the original project while modernising the ESPHome configuration and packaging structure.

## Features

- Native Tuya fan integration
- Fan speed control
- Fan direction control
- Fan mode selection
  - Normal
  - Eco
  - Sleep
- Fan timer selection
  - Off
  - 1-12 Hours
- Tuya light support
- Estimated fan power monitoring
- Estimated light power monitoring
- Optional NTC temperature sensor
- Optional TMP117 temperature sensors
- Wi-Fi RSSI diagnostics
- GitHub-hosted ESPHome package
- Minimal per-device configuration

## Installation

Create a new ESPHome device and use the following configuration:

```yaml
substitutions:
  fan_name: Music Room Fan
  fan_model: "SKY1203"

packages:
  skyfandc: github://ryandenyer/SkyfanDC/skyfandc.yaml@main

esphome:
  name: musicroomfan
  friendly_name: Music Room Fan

esp8266:
  board: d1_mini

logger:
  baud_rate: 0

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

api:
  encryption:
    key: !secret api_key

ota:
  - platform: esphome

captive_portal:
```

## Supported Fan Models

Set the fan model to enable estimated power monitoring.

```yaml
substitutions:
  fan_model: "SKY1203"
```

Supported models:

```text
SKY903
SKY1203
SKY1303
SKY1503
SKY1204
SKY1404
```

## Available Entities

### Fan

- Fan
- Speed control
- Direction control

### Selects

- Mode
- Timer

### Light

- On/Off
- Brightness

### Optional Sensors

Disabled by default in Home Assistant:

- Fan Power
- Light Power
- NTC Temperature
- TMP117 Temperatures
- Wi-Fi RSSI

## Default Datapoints

```text
DP1   Fan Power
DP2   Fan Mode
DP3   Fan Speed
DP8   Fan Direction
DP15  Light Power
DP16  Light Brightness
DP22  Timer
```

Override any datapoint in your device configuration:

```yaml
substitutions:
  dp_power: "1"
  dp_speed: "3"
  dp_direction: "8"

  dp_mode: "2"
  dp_timer: "22"

  dp_light: "15"
  dp_light_dimmer: "16"
```

## Package Structure

```text
SkyfanDC/
│
├── defaults.yaml
├── skyfandc.yaml
│
└── packages/
    ├── mode_select.yaml
    ├── timer_select.yaml
    ├── tuya_fan.yaml
    ├── tuya_light.yaml
    ├── sensor_power_fan.yaml
    ├── sensor_power_light.yaml
    ├── sensor_ntc.yaml
    ├── sensor_tmp117.yaml
    └── sensor_rssi.yaml
```

## Defaults

```yaml
fan_model: "SKY1203"

speed_count: "5"

dp_power: "1"
dp_speed: "3"
dp_direction: "8"

dp_mode: "2"
dp_timer: "22"

dp_light: "15"
dp_light_dimmer: "16"

light_max_power: "20"
```

## Home Assistant

After configuration and provisioning, Home Assistant will automatically discover:

- Fan
- Light
- Mode Select
- Timer Select

Additional sensors are included but disabled by default to minimise entity clutter.

## Fan Power Modelling

Fan power values are estimated from the original SkyFan DC datasheet specifications and scaled for the 5-speed ESPHome implementation.

### SKY903

```text
0.0, 3.4, 5.7, 10.0, 18.0, 32.0
```

### SKY1203

```text
0.0, 4.0, 6.4, 12.2, 20.6, 32.5
```

### SKY1303

```text
0.0, 4.3, 7.1, 13.0, 23.3, 31.8
```

### SKY1503

```text
0.0, 4.3, 7.2, 13.2, 24.0, 44.2
```

### SKY1204

```text
0.0, 4.2, 7.1, 13.8, 25.0, 30.0
```

### SKY1404

```text
0.0, 3.9, 6.5, 12.2, 21.4, 38.0
```

## Disclaimer

This project is not affiliated with Ventair, Tuya, or Egglec.

This repository is a community-maintained ESPHome package derived from the original SkyFanDC project by James Eggleston.

## License

Please refer to the original project for licensing information and attribution requirements.