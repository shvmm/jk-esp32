# jk-esp32
# ESPHome Web server for monitoring JK-BMS via UART instead of BLE.
This project is a fork of excellent JK-BMS monitoring project from https://github.com/syssi/esphome-jk-bms

I have only simpliefied things for very particular plug and play use case.

Tested on: JK-BD6A24S10P (but should work on any jk bms). Read main project esphome-jk-bms for more details.
ESPHome version: 2023.10.3, compiled using Windows 11

Requirements:
DOIT ESP32 DEVKITv1 board
GPIO ribbon
JST 1.25mm 4 pin connector for JK-BMS

You can prepare the cable according to this collage if you want!


![Preparation collage](/images/steps-collage.jpg?raw=true "Preparation Collage")

There are three Steps involved:

a. Configuring the code for your particular setup.

b. Preparing your ESP32 board by compiling and flashing the code.

c. Connecting the configured ESP32 to your BMS UART-TTL port and use the web-server IP for monitoring.

![DOIT ESP32 DEVKITv1 PINOUT](/images/ESP32-DevKit-V1-Pinout-Diagram-r0.1-CIRCUITSTATE-Electronics-2.png?raw=true "DOIT ESP32 DEVKITv1 PINOUT")

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
The RX pin of BMS must be connected to TX2 pin of ESP32 board and vice versa.
Just swap the data pins, if BMS not detected in first try.



# a. Configuring the code for your setup

0. Install CP210x Universal Windows Driver
  https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads
1. Download and install python from https://www.python.org/downloads/

Remember to tick all boxed during installation for path name limit and environment variables for ease of use.

2. Open CMD and run
   ```
   pip install esphome
   ```

3. Download the release and extract it to a folder.
  Open secrets.yaml file in the main directory to edit your WIFI SSID and password.
  Comment and uncomment needed/unneeded sensors in the configuration file.
  If you have a newer BMS, change to newer protocol.
5. Right click -> choose Open in Terminal
6. enter the command
    ```
    esphome run .\esp32-example.yaml
    ```
7. After compilation is finished, you may be asked to enter the COM port of your ESP32 board. Press 1
8. Make connections accordingly.
9. 
