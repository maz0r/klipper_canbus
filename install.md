# CANBUS TOOLHEAD INSTALL

Assumptions

- A working instance of Klipper, Moonraker and / or Mainsail/Fluidd and all pre-requisits
- Access to the Raspberry PI terminal (SSH or physical keyboard/mouse)
- A CAN adapter (USB or SPI)
  - Waveshare RS485 (Serial)
  - MKB Canable / Canable Pro (USB)
  - UTOC-1/3
  - Other... (some things may vary)
- A CAN toolhead board
  - Huvud
  - SHT36/42
  - TurboCAN

## Initial Setup



Canbus wiring

![](images/canbus_wiring.svg)



### RS485 SPECIFIC

/boot/cmdline.txt

```bash
do stuff
```



/boot/config.txt

``` bash
do stuff
```





#### Setting up the CAN0 network

A canbus 

```bash
sudo nano /etc/network/interfaces.d/can0
```



```bash
auto can0
iface can0 can static
    bitrate 500000
    up ifconfig $IFACE txqueuelen 128

```



**Add a startup rule** *(this is to rc.local, I tried systemd but couldnt get the syntax)*

```bash
sudo sed -i '/^exit\ 0$/i \ifconfig can0 down\nip link set can0 type can bitrate 500000\nip link set can0 txqueuelen 256\nifconfig can0 up' /etc/rc.local
```



*Reboot*

```bash
sudo reboot
```







### Firmware configuration



```
!!!! Enable extra config options!!!!
- Enable Micro-controller Architecture (STMicroelectronics STM32)
- Pick STM32F103
- Pick Bootloader offset (2KiB bootloader (HID Bootloader))
- Disable Use USB for communication (instead of serial)
- Enable Use CAN for communication (instead of seria)l
!!!! Pick CAN pins (Pins PB8(rx) and PB9(tx)) !!!!
```

### 

### Bootloader and Flashing

The boards come preloaded with the HID bootloader for flashing over USB. Note that the board can not be powered over USB.

To enter the bootloader pin BOOT1 must be connected to  3.3V when the board is powered up or reset. When in the bootloader the  green LED will flash quickly. Flash with the command "make flash  FLASH_DEVICE=1209:beba"

Hopefully a CAN capable bootloader will be developed to allow flashing over CAN bus.





ifconfig can0

sudo reboot



ifconfig can0



### Flashing the MCU

connect the huvud to your pi via USB



### Validation

PI W2 - BTT PICO - UART - MKS CANABLE PRO - HUVUD 0.61

PI 4B - BTT PICO - USB - Waveshare RS485 CAN HAT







?? can-utils

