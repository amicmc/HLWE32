# HLWE32

Due to bad supported new boards offered by Heltec I've __frankesteinized__ these two repos for my own use:

- https://github.com/eiannone/Heltec_Esp32_LoRaWan
- https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series/tree/master/esp32/libraries/LoraWan102

Feel free to do with this whatever you want or can.
In order to use this library, you will need to know that there's an issue in Espressif platform related to the new Heltec boards. The support for them has been merged by GitHub user [Baptou88](https://github.com/Baptou88/platform-espressif32) (thanks Baptou88!). It is related to the boards pinout and may be that when you read this the issue is solved. So, if you get connectivity problems, it may be you can solve them locating and modifying your local copy of the file ```pins_arduino.h```. These are the relevant lines:  

```c
...
/* 
$HOME/.platformio/packages/framework-arduinoespressif32/variants/heltec_wifi_lora_32_V3/pins_arduino.h
*/
// #define WIFI_LoRa_32_V3 true
...
static const uint8_t SDA = 41;
static const uint8_t SCL = 42;

static const uint8_t SS    = 8;
static const uint8_t MOSI  = 10;
static const uint8_t MISO  = 11;
static const uint8_t SCK   = 9;
...

```
When done you can use this example:

```dosìni
; platformio.ini
;
; PlatformIO Project Configuration File
;
;   Build options: build flags, source filter
;   Upload options: custom upload port, speed and extra flags
;   Library options: dependencies, extra library storages
;   Advanced options: extra scripting
;
; Please visit documentation for the other options and examples
; https://docs.platformio.org/page/projectconf.html

[env:heltec_wifi_lora_32_v3]
platform = https://github.com/Baptou88/platform-espressif32
board = heltec_wifi_lora_32_V3
framework = arduino
monitor_speed = 115200
monitor_filters = log2file, time, default, esp32_exception_decoder
build_flags =
    -D REGION_EU868
    -D ACTIVE_REGION=LORAMAC_REGION_EU868
    -D LoRaWAN_DEBUG_LEVEL=1
    -D LORAWAN_PREAMBLE_LENGTH=8
    -D WIFI_LoRa_32_V3

lib_deps=https://github.com/amicmc/HLWE32
```
We've got a bunch of Heltec WiFi LoRa ESP32 based boards (v.2.1 and v3) and they are working now. 
