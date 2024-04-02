# Notes

## Build Instructions (for Arduino IDE)

It is **not** quite straightforward to set up an environment to build the Morserino-32 binary code from the source.

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

## Install Arduino IDE

* Legacy Arduino IDE 1.8.19
  ** tested on MacOS 13.5 (Ventura)
* Arduino IDE 2.3.2
  ** tested on MacOS 13.5 (Ventura)
  ** tested on Linux (Fedora 39)

## Install Heltec Library

Two parts:

1. Heltec ESP32 development framework (https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series)
2. Heltec ESP32 library (https://github.com/HelTecAutomation/Heltec_ESP32)
 
### Install Heltec ESP32 development framework

Install version 0.0.6 of the development framework via **git**.

https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series/releases/tag/0.0.6

#### MacOS

https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series/blob/master/InstallGuide/mac.md

Arduino 1.8.x:

```
cd ~/Documents/Arduino/hardware
```

Arduino 2.x.x:

```
cd ~/Library/Arduino15/packages  # Mac
cd ~/.arduino15/packages         # Linux
```

The rest is identical for both IDE versions.

```
git clone https://github.com/Heltec-Aaron-Lee/WiFi_Kit_series.git --branch 0.0.6
mv WiFi_Kit_series heltec
cd heltec
git submodule set-url esp8266/libraries/LittleFS/lib/littlefs https://github.com/lorol/LITTLEFS.git
git submodule update --force --recursive --init --remote
cd esp32/tools
python3 get.py
```

### Install Library

```
cd ~/Documents/Arduino/libraries # Mac
cd ~/Arduino/libraries           # Linux
git clone https://github.com/HelTecAutomation/Heltec_ESP32.git --branch 1.0.9
```

**NOTICE: the Arduino IDE 2.x.x checks for updates when it starts. Do not hit the
default "INSTALL ALL" button. This would overwrite the Heltec library.**

## Install ArduinoJson

Install ArduinoJson 6.20.1 via Arduino library manager.

# Build using Arduino gui

```
cd <path-to-source>/Morserino-32/Software/src
mv 'Version 5' m32_v5
```

In gui:

* set board: WiFi LoRa 32(V2)
* set upload speed: 115200
* set CPU frequency: 240 Mhz
* set LoRaWan Region: REGION_EU433

In case you get this error:

```
exec: "python": executable file not found in $PATH
Error compiling for board WiFi LoRa 32(V2).
```

Fix the path to the python executable:

```
cd ~/Documents/Arduino/hardware/heltec/esp32
perl -pli.orig -e 's|python|/path/to/python|' platform.txt
```

Compile. Log output:

```
[...]
Sketch uses 1149634 bytes (34%) of program storage space. Maximum is 3342336 bytes.
Global variables use 124432 bytes (37%) of dynamic memory, leaving 203248 bytes for local variables. Maximum is 327680 bytes.
```

# Build using cli

TODO
