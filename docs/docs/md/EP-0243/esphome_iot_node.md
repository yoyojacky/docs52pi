# ESPHome IoT Node with ESP32-S3 

* Product SKU: EP-0243
* Product Name: ESPHome IoT Node  with ESP32-S3 

## Description

Introducing the ESPHome IoT Node, a powerful development board based on the ESP32-S3 chipset. This board is designed for IoT enthusiasts and developers looking to create smart home devices with ease. With its versatile features, it offers a seamless integration with various smart home ecosystems.

### Key Features

- **ESP32-S3 Chip**: High-performance microcontroller for IoT applications.

- **USB-C Programming and Power Supply**: Convenient for both programming and power supply.

- **DC 5521 Power Jack**: Accepts input voltage from 9V to 12V for stable operation.

- **OV5640CSP Camera Module**: Integrated 5-megapixel camera with a 20MHz driving frequency.

- **Resolution Flexibility**: Switch between 640x480 VGA (4:3) and 160x120 QQVGA (4:3) modes.

- **ST7789V IPS Display**: 1.3-inch RGB display with 240x240 pixels for clear visual feedback.

- **52Pi Compatibility**: Works with 52Pi watering kits, including screen and relay modules.

- **ESPHome Integration**: Easy deployment without coding using the ESPHome framework.

- **OTA Updates**: Remote firmware updates via ESPHome's OTA feature once networked.

- **Home Assistant Integration**: Seamless integration for remote control and video monitoring.

## Application Scenarios

1. **Smart Home Automation**: Control home appliances, lighting, and security systems.

2. **Video Surveillance**: Set up a home security camera with remote monitoring capabilities.

3. **IoT Projects**: Develop custom IoT projects with remote firmware updates and easy configuration.

4. **Home Gardening**: Automate watering systems with the integrated 52Pi watering kit compatibility.

5. **DIY Smart Devices**: Create personalized smart devices with customizable features and remote access.

## Getting Started

- **Initial Firmware Flashing**: Use the official ESP32 flashing software for the first-time firmware installation.

- **Network Connection**: Once connected to the network, leverage ESPHome for remote OTA updates.

- **Configuration**: Edit YAML configuration files online to customize your device without complex coding.

## Why Choose ESPHome IoT Node?

- **Simplicity**: Easy to use with zero coding required for basic setups.

- **Flexibility**: Adaptable to various IoT applications and smart home integrations.

- **Powerful**: Harness the capabilities of the ESP32-S3 chipset for robust performance.

- **Community Support**: Benefit from the extensive ESPHome and Home Assistant communities for support and resources.

Experience the future of smart home technology with the ESPHome IoT Node, where innovation meets convenience.

## Setting Up the Environment

* A Detailed Guide

Let's dive into the process of setting up your development environment step by step.

## 















usb-c 编程口，供电。
DC 5521 max power: 12v, min power: 9v
camera: ov5640CSP 500Mpixels camera clock 20Mhz 
resolution (Optional, enum): The resolution the camera will capture images at. Higher resolutions require more memory, if there’s not enough memory you will see an error during startup.

160x120 (QQVGA, 4:3)

176x144 (QCIF, 11:9)

240x176 (HQVGA, 15:11)

320x240 (QVGA, 4:3)

400x296 (CIF, 50:37)

640x480 (VGA, 4:3, default)

    frequency: 20MHz
  i2c_pins:
    sda: GPIO9
    scl: GPIO10
  data_pins: [GPIO38, GPIO40, GPIO41, GPIO39, GPIO21, GPIO16, GPIO17, GPIO18]
  vsync_pin: GPIO19
  href_pin: GPIO8
  pixel_clock_pin: GPIO47
  reset_pin: GPIO11 
  enable_pin: PWDOWN connected to PCF8574's IO3  (HIGH LEVEL: disable, LOW
          LEVEL: enable) 

  1.3 Inch RGB 240x240: controller chip is ST7789V, spi 协议，
  spi:
  clk_pin: GPIO12
  mosi_pin: GPIO46
  1Mhz, display:
  - platform: st7789v
    model: Adafruit Funhouse 240x240
    cs_pin: GPIO42
    dc_pin: GPIO48
    reset_pin: GPIO0
    lambda: |-
      it.image(0, 0, id(my_image));

PCF8574: EXPAND I/O VIA I2C PROTOCL, 0X38 DEFAULT ADDRESS
控制摄像头开关，还有3个继电器，板载1个LED， 扩展2个LED，引脚需要确认。 
IO0-IO2 需要inverted :true 控制。 

IR receiver 

lg: Decode and dump LG infrared codes.
nec: Decode and dump NEC infrared codes.

remote_receiver:
  pin:
    number: GPIO15
    inverted: True
    mode:
      input: true
      pullup: true
  dump: lg  或者 NEC 
  rmt_channel: 4
