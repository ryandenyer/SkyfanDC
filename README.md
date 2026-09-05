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
  fan_name: SkyFan DC
  fan_model: "SKY1203" #change to your fan model

packages:
  skyfandc: github://ryandenyer/SkyfanDC/skyfandc.yaml@main

esphome:
  name: skyfandc
  friendly_name: SkyFan DC

esp8266:
  board: d1_mini

logger:
  baud_rate: 0

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  ap:

api:
  encryption:
    key: !secret api_key

ota:
  - platform: esphome

captive_portal:
```

## Customization

### Fan Name

The `fan_name` substitution controls the names of all entities created by the package.

Example:

```yaml
substitutions:
  fan_name: Master Bedroom Fan
```

This will create entities such as:

```text
Master Bedroom Fan
Master Bedroom Fan Light
Master Bedroom Fan Mode
Master Bedroom Fan Timer
Master Bedroom Fan Power
Master Bedroom Fan RSSI
```

### Fan Model

The `fan_model` substitution selects the power curve used for estimated fan power monitoring.

Example:

```yaml
substitutions:
  fan_model: "SKY1503"
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

### Datapoints

Most installations use the default datapoints and require no changes.

Override them only if your controller uses different values:

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

### Optional Settings

Additional package settings can also be overridden:

```yaml
substitutions:
  light_max_power: "20"

  ntc_vcc_pin: "14"
  ntc_adc_pin: "17"

  i2c_sda_pin: "GPIO4"
  i2c_scl_pin: "GPIO5"

  tmp117_update_interval: "60s"
```

### Example

```yaml
substitutions:
  fan_name: Outdoor Fan
  fan_model: "SKY1404"

packages:
  skyfandc: github://ryandenyer/SkyfanDC/skyfandc.yaml@main
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

ntc_vcc_pin: "14"
ntc_adc_pin: "17"

i2c_sda_pin: "GPIO4"
i2c_scl_pin: "GPIO5"

tmp117_update_interval: "60s"
```

## Home Assistant

After configuration and provisioning, Home Assistant will automatically discover:

- Fan
- Light
- Mode Select
- Timer Select

Additional sensors are included but disabled by default to minimise entity clutter.

## Home Assistant Entity Categories

### Primary Entities

- Fan
- Light
- Mode
- Timer

### Diagnostic Entities

Disabled by default:

- Wi-Fi RSSI
- TMP117 Sensors
- Temperature Monitoring
- Estimated Power Sensors

## Disclaimer

This project is not affiliated with Ventair, Tuya, or Egglec.

This repository is a community-maintained ESPHome package derived from the original SkyFanDC project by James Eggleston.

## License

Please refer to the original project for licensing information and attribution requirements.