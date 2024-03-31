# Notes

## How to compile?

From groups.io thread [Compiling from source](https://morserino.groups.io/g/main/topic/compiling_from_source/104750585?p=,,,20,0,0,0::recentpostdate/sticky,,,20,2,20,104750585,previd%3D1710572933441364752,nextid%3D1708351118178241033&previd=1710572933441364752&nextid=1708351118178241033)

> Willi, OE1WKL:
>
> The problem is that Heltec moved their resources around, and they
> are sometimes hard to find.
>
> The easiest way with the Arduino environment is to install the heltec
> library directly from Arduino’s library manager. The library is called
> „Heltec ESP32 Dev-Boards“, and I am using version 1.0.9 (newer
> versions might give problems and at a minimum require code changes).
>
> The other library you will need for version 5.x is ArduinoJson by
> B. Blanchon (I am suing V. 6.20.1, but newer versions probably work ok).

## Install Legacy Arduino (1.8.x)

Download Legacy Arduino IDE 1.8.19. Do not use the current 2.x.x.

## Install Heltec Library

This is tricky.

https://github.com/HelTecAutomation/Heltec_ESP32

> This library requires installation of the [Heltec ESP32 development framework](https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series)! A detailed document about how to install the Heltec ESP32 development
> framework and this library available here:
>
> [Heltec ESP32+LoRa Series Quick Start — esp32 latest documentation](https://docs.heltec.org/en/node/esp32/esp32_general_docs/quick_start.html)

### Install Heltec ESP32 development framework

https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series/releases/tag/0.0.6

Download esp32-0.0.6.zip

cd ~/Documents/Arduino/hardware/heltec
unzip ~/Downloads/esp32-0.0.6.zip
mv esp32-0.0.6 esp32



Install the development framework via git so we can pick an older version.

On Mac:

https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series/blob/master/InstallGuide/mac.md

cd ~/Documents/Arduino/hardware
git clone https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series.git --branch 0.0.6
mv WiFi_Kit_series heltec
cd heltec

git submodule set-url esp8266/libraries/LittleFS/lib/littlefs https://github.com/lorol/LITTLEFS.git

cd esp32/tools
python3 get.py

```
Submodule 'esp32/libraries/ESP32_AzureIoT_Arduino' (https://github.com/VSChina/ESP32_AzureIoT_Arduino.git) registered for path 'esp32/libraries/ESP32_AzureIoT_Arduino'
Submodule 'esp8266/libraries/ESP8266SdFat' (https://github.com/earlephilhower/ESP8266SdFat.git) registered for path 'esp8266/libraries/ESP8266SdFat'
Submodule 'esp8266/libraries/LittleFS/lib/littlefs' (https://github.com/esp8266/Arduino/libraries/LittleFS.git) registered for path 'esp8266/libraries/LittleFS/lib/littlefs'
Submodule 'esp8266/libraries/SoftwareSerial' (https://github.com/PaulStoffregen/SoftwareSerial.git) registered for path 'esp8266/libraries/SoftwareSerial'
Cloning into '/Users/andreas/Documents/Arduino/hardware/heltec/esp32/esp32/libraries/ESP32_AzureIoT_Arduino'...
Cloning into '/Users/andreas/Documents/Arduino/hardware/heltec/esp32/esp8266/libraries/ESP8266SdFat'...
Cloning into '/Users/andreas/Documents/Arduino/hardware/heltec/esp32/esp8266/libraries/LittleFS/lib/littlefs'...
remote: Not Found
fatal: repository 'https://github.com/esp8266/Arduino/libraries/LittleFS.git/' not found
fatal: clone of 'https://github.com/esp8266/Arduino/libraries/LittleFS.git' into submodule path '/Users/andreas/Documents/Arduino/hardware/heltec/esp32/esp8266/libraries/LittleFS/lib/littlefs' failed
Failed to clone 'esp8266/libraries/LittleFS/lib/littlefs'. Retry scheduled
Cloning into '/Users/andreas/Documents/Arduino/hardware/heltec/esp32/esp8266/libraries/SoftwareSerial'...
Cloning into '/Users/andreas/Documents/Arduino/hardware/heltec/esp32/esp8266/libraries/LittleFS/lib/littlefs'...
remote: Not Found
fatal: repository 'https://github.com/esp8266/Arduino/libraries/LittleFS.git/' not found
fatal: clone of 'https://github.com/esp8266/Arduino/libraries/LittleFS.git' into submodule path '/Users/andreas/Documents/Arduino/hardware/heltec/esp32/esp8266/libraries/LittleFS/lib/littlefs' failed
Failed to clone 'esp8266/libraries/LittleFS/lib/littlefs' a second time, aborting
```

### Install Libary

cd ~/Documents/Arduino/libraries
git clone https://github.com/HelTecAutomation/Heltec_ESP32.git --branch 1.0.9


## ArduinoJson

Install ArduinoJson 6.20.1 via Arduino library manager.


# Build using gui

rename "Version 5"

Set Board to


Arduino: 1.8.19 (Mac OS X), Board: "WiFi LoRa 32(V2), 240MHz (WiFi/BT), 921600, None, REGION_EU868, CUSTOM, None"

```
Multiple libraries were found for "WiFi.h"
 Used: /Users/andreas/Documents/Arduino/hardware/heltec/esp32/libraries/WiFi
 Not used: /Applications/Arduino.app/Contents/Java/libraries/WiFi
exec: "python": executable file not found in $PATH
Error compiling for board WiFi LoRa 32(V2).


This report would have more information with
"Show verbose output during compilation"
option enabled in File -> Preferences.
```

patch


vi /Users/andreas/Documents/Arduino/hardware/heltec/esp32/platform.txt
change to python3

# Build using cli

