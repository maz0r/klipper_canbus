# CANBUS TOOLHEAD INSTALL

Assumptions

- A working instance of Klipper, Moonraker and / or Mainsail/Fluidd
- Access to the Raspberry PI terminal (via SSH or physical keyboard/mouse/display)
- A CAN adapter (USB or SPI)
  - Waveshare RS485 (Serial)
  - MKB Canable / Canable Pro (USB)
  - UTOC-1/3
  - Other... (some things may vary)
- A CAN toolhead board
  - Huvud
  - SHT36/42
  - TurboCAN
- This guide and a brew (or coffee if you must)
  

## **IMPORTANT**

Each controller page has a set of "safe" default settings which should work for the majority of users, you should initially setup your controller based on these values as these will inform some of the settings to be used for your Toolhead board of choice *i.e. the bitrate*


## Overview
### What is Canbus

CANbus is vehicle standard that allows for communication between multiple devices on a single network (multiplex wiring). The protocol has been used in Automotive applications since the early 90's and it's ubiquitous in modern vehicles.

Want to know more: [https://en.wikipedia.org/wiki/CAN_bus](https://en.wikipedia.org/wiki/CAN_bus)

### Why do I want it

Wires be heavy yo.


### *A simplified overview of Canbus wiring*

![<img src='./images/canbus_wiring.svg'>](images/canbus_wiring.svg)

- [ ] Explain termination
- [ ] Highlight where different controller/board combinations may be wired differently (termination/ground/voltage passthrough etc).

***


## Control boards

[canable](./controller/canable.md) 

[<img src='./images/mks_canable.jpg' width='250'>](/controller/canable.md)


[can2usb](./controller/usb2can.md)

[<img src='./images/usb2can.jpg' width='250'>](/controller/usb2can.md)

[rs485 (waveshare)](./controller/rs485.md)

[<img src='./images/waveshare_485.jpg' width='250'>](/controller/rs485.md)

[utoc](./controller/utoc1-3.md)

[<img src='./images/utoc-1.jpg' width='250'>](/controller/utoc1-3.md)


## Toolhead boards

[huvud](./toolhead/huvud-0.61.md)

[<img src='./images/huvud_0.61.png' width='250'>](./toolhead/huvud-0.61.md)


[SHTXX](./toolhead/sht36-42.md)

[<img src='./images/sht36.jpg' width='250'>](./toolhead/sht36-42.md)
[<img src='./images/sht42.jpg' width='250'>](./toolhead/sht36-42.md)


[TurboCAN](./toolhead/turbocan.md)

[<img src='./images/turbocan.jpg' width='250'>](./toolhead/turbocan.md)





