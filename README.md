# Clean/Polished ESPHome Web server for monitoring JK-BMS via UART instead of BLE.
This project is a fork of excellent JK-BMS monitoring project from https://github.com/syssi/esphome-jk-bms
This project also contains a polished CANBUS implementation from https://github.com/Sleeper85/esphome-jk-bms-can
The filename is esp32-jk-bms-can.yaml

I have only simpliefied things for a very particular 'plug and play' use case.

![Demo Picure](/images/IMG_20231030_154612.jpg "Demonstration")

Tested on: JK-BD6A24S10P (but should work on any JK BMS). Read main project [ESPHome JK BMS](https://github.com/syssi/esphome-jk-bms "Demonstration") for more details.
ESPHome version: 2023.10.3, Windows 11

## 1. Requirements:
1. Any cheaply available ESP32 board
2. GPIO ribbon connectors
3. JST 1.25mm 4 pin connector for JK-BMS

You can easily prepare the BMS and GPIO cable accordingly if you want!

![Preparation collage](/images/steps-collage.jpg?raw=true "Preparation Collage")

There are three Steps involved:

a. Configuring the code for your particular setup.

b. Preparing your ESP32 board by compiling and flashing the code.

c. Connecting the configured ESP32 to your BMS UART-TTL port and using the web-server IP for monitoring.
```
┌──────────┐                ┌─────────┐
│          │<----- RX ----->│         │
│  JK-BMS  │<----- TX ----->│ ESP32/  │
│          │<----- GND ---->│         │<---- USB Power Supply
└──────────┘                └─────────┘

# UART-TTL socket (4 Pin, JST 1.25mm pitch)
┌─── ─────── ────┐
│                │
│ O   O   O   O  │
│GND  RX  TX VBAT│
└────────────────┘
  │   │   │
  │   │   └─── GPIO16 (`RX2_pin`)
  │   └─────── GPIO17 (`TX2_pin`)
  └─────────── GND
```
Just swap the RX and TX pins, if BMS is undetected.



## 2. Configuring the code for your setup:


0. Install CP210x Universal Windows Driver
  https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads
1. Download and install python from https://www.python.org/downloads/
  Remember to tick all boxed during installation for path name limit and environment variables for ease of use.
2. Open CMD and run
   ```
   pip3 install esphome
   ```
   
3. You can check whether esphome is installed by running

   ```
   esphome version
   ```
4. Download the release and extract it to a folder.
  Open secrets.yaml file in the main directory to edit your WIFI SSID and password.
5. Comment and uncomment needed/unneeded sensors in the configuration file.
  If you have a newer BMS, you may need to change to a newer protocol.
6. Right click -> choose Open in Terminal
  Enter the command
    ```
    esphome run .\esp32-example.yaml
    ```
7. After compilation is finished, you may be asked to enter the COM port of your ESP32 board. Press 1 to confirm
8. Make the connection between the BMS and ESP32 and connect a USB power supply.
9. The IP for the webserver will be displayed in ESP32 serial log after successful connection to WIFI has been made.
