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

![<img src='./images/canbus_wiring.jpg'>](images/canbus_wiring.jpg)

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

## Special Bootloaders (Optional)

[canboot](./controller/canboot.md)

[<img src='./images/canboot.png' width='250'>](./controller/canboot.md)

## Toolhead boards

[huvud](./toolhead/huvud-0.61.md)

[<img src='./images/huvud_0.61.png' width='250'>](./toolhead/huvud-0.61.md)


[SHTXX](./toolhead/sht36-42.md)

[<img src='./images/sht36.jpg' width='250'>](./toolhead/sht36-42.md)
[<img src='./images/sht42.jpg' width='250'>](./toolhead/sht36-42.md)


[TurboCAN](./toolhead/turbocan.md)

[<img src='./images/turbocan.jpg' width='250'>](./toolhead/turbocan.md)



## Connecting your controller to your Toolhead board

.. stub with just text for now but will add diagrams for various configurations.

.. termination resistors

### RS485 / Waveshare HAT

The Waveshare CAN HAT has an integrated termination and it's best practice to add pullup at the toolhead.

- H on the Waveshare to H on the toolhead
- L on the Waveshare to L on the toolhead
- 12/24v from PSU 12/24v on Toolhead 
- GND from PSU oo toolhead

### UTOC-1 / UTOC-3

- USB from the PI to the UTOC board
- H on UTOC to H on toolhead
- L on UTOC to L on toolhead
- 24V from  PSU to UTOC
- GND from PSU to UTOC
- 24 on UTOC to 24 on toolhead
- GND on UTOC to GND on toolhead

### CANABLE / CANABLE PRO

#### Normal

`<no image>`

- USB from the PI
- GND from PSU to GND on the CANABLE
- GND from PSU to GND on toolhead 
- 12/24v from PSU to 12/24v on toolhead 
- H from Canable to H on toolhead 
- L from Canable to L on toolhead

#### Termination resistors



Standard controller termination
`<no image>`

*There are two jumpers near the green port, bridge the furthest two along the edge of the boad*

Pro Controller termination

[<img src='./images/mks_canable_terminated.jpg' width='250'>](./images/mks_canable_terminated.jpg)



### Terminations

While noit compulsary it is useful to have terminations at both ends of a the can bus (note if chaining multiple devices only the START and END of the bus need termiations.)
#### HUVUD Termination

There is no 120ohm resistor on the board, you can solder your own SMT style resistor using the designated pads (shown below)

[<img src='./images/huvud_0.61_termination.jpg' width='250'>](./images/huvud_0.61_termination.jpg)


#### SHTXX Termination

The SHT boards include termination resistors and jumpers.
So simply bridge the green pins is per the images below.

##### 36

[<img src='./images/sht36_terminated.jpg' width='250'>](./images/sht36_terminated.jpg)

##### 42
 
[<img src='./images/sht42_terminated.jpg' width='250'>](./images/sht42_terminated.jpg) 
