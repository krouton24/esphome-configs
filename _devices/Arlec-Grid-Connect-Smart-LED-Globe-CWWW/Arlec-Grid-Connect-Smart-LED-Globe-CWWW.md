---
title: Arlec Grid Connect Smart LED Globe CWWW (GLD112HA)
date-published: 2020-04-13
type: light
standard: au
---

As per the [Arlec Grid Connect Smart LED Globe RGB](https://esphome-configs.io/devices/arlec-grid-connect-smart-led-globe-rgb/), these globes are sold at Bunnings in Australia and New Zealand and can be converted using tuya-convert.

However unlike the RGB version these appear to use a BP5926 chip to drive the LED's and this chip uses a PWM signal so set the colour temperature rather than a PWM signal for each colour channel.

To get these globes to work, a Custom Component is required due to the BP5926 chip that they have used to drive the LED's.

Copy the 4 files from ssieb's repo [here](https://github.com/ssieb/custom_components/tree/master/cwww2) and place them in the cwww2 folder you just created.

```
esphome:
  name: arlec_white_1
  platform: ESP8266
  board: esp01_1m

wifi:
  ssid: "your ssid"
  password: "password"
  manual_ip:
    static_ip: xxx.xxx.xxx.xxx
    gateway: xxx.xxx.xxx.xxx
    subnet: xxx.xxx.xxx.xxx

  ap:
    ssid: "your fallback ssid"
    password: "password"

output:
  - platform: esp8266_pwm
    id: output1
    pin: GPIO5
  - platform: esp8266_pwm
    id: output2
    pin: GPIO13

light:
  - platform: cwww2
    id: lightid
    name: "Light CWWW"
    color_temperature: output2
    brightness: output1
    cold_white_color_temperature: 6500 K
    warm_white_color_temperature: 3000 K
    
    restore_mode: ALWAYS_OFF
```
