### Huvud Firmware

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

#### Wiring

Wire the boards up like so

![](images/huvud_flash_wiring.svg)



####

The boards come preloaded with the HID bootloader for flashing over USB. Note that the board can not be powered over USB.

To enter the bootloader pin BOOT1 must be connected to  3.3V when the board is powered up or reset. When in the bootloader the  green LED will flash quickly. Flash with the command "make flash  FLASH_DEVICE=1209:beba"

Hopefully a CAN capable bootloader will be developed to allow flashing over CAN bus.


