# xmaslights
Simple project to control 433mhz transmitter from the web using an Arduinio Uno and an Adafruit CC3300 WIFI shield.

## Configuration
Set the strings that are required to switch on and switch off the lights, you can find these codes by setting up a receiver and pressing the buttons on your remote [https://github.com/sui77/rc-switch/wiki/HowTo_Receive](https://github.com/sui77/rc-switch/wiki/HowTo_Receive).  

```c
void switchOff(void) {
  Serial.println("Off");
  mySwitch.send("000000000000000000010100");
  mySwitch.send("000000000100000000010100");
}

void switchOn(void) {
  Serial.println("On");
  mySwitch.send("000000000000000000010101");
  mySwitch.send("000000000100000000010101");
}
```

You also need to configurure your firewall to pass port 8099 through to your arduino ip address, the address is shown in the serial connection when the arduino boots.  I recommend setting your router to assign a reserved ip address for the arduino's mac address.

## Building
This project can be built with [platformio.org](http://platformio.org) or the standard Arduino software.  

### Arduino IDE
To build with Arduino IDE copy the folders in the lib folder to your Arduino library then set the two constants in the Lights.ino file.

```c
#define WLAN_SSID       "SSID"
#define WLAN_PASS       "password"
```

### Platformio
```bash
PLATFORMIO_SRC_BUILD_FLAGS='-DWLAN_SSID=\"SSID\" -DWLAN_PASS=\"password\"' pio run -t upload  
```

Platformio will add the define lines in the source code automatically if the build flags are set.

## Running
When everything is up and running you can switch your lights on and off by accessing the following URLs:  
* http://arduino-ip:8099/on
* http://arduino-ip:8099/off
