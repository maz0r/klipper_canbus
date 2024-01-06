# Manta M5P with CAN Bus

The Manta M5P is capable of CANBus but in the vendor manual that comes with it, it makes absolutely no mention of how to use CAN bus with it. It is possible though and the Manta M5P can be used to connect to a CAN bus toolhead board such as an EBB36 without the use of an additional U2C board, since it itself is already a U2C board.

## Hardware Setup

1. Put a jumper on the 120R termination pins as shown here
[pic]
2. Connect your CAN cable to your toolhead as shown like this. GREEN is CAN Low and YELLOW is CAN High.
[pic]
3. Assuming you followed Step 2, connect the GREEN and YELLOW wires to the following pins on the Manta M5P.
[pic]
4. And connect the power pins to these.
[pic]
5. Ensure that your toolhead board (EBB36 or so) has the 120R Jumper connected. Pic for example:
[pic]
6. Leave your toolhead board disconnected first from the Manta M5P, and proceed to the software steps for now. Prepare your cabling and connectors so that in step 21 of the Software Steps you can connect your toolhead board and continue with the setup.

## Software Steps

1. Go to your home directory `cd ~`
2. Download the CanBoot repo if you have not already `git clone https://github.com/Arksine/CanBoot.git`
3. Go into the CanBoot repo directory `cd ~/CanBoot`
4. Configure the CanBoot firmware `make menuconfig`

```
    Micro-controller Architecture (STMicroelectronics STM32)  --->
    Processor model (STM32G0B1)  --->
    Build CanBoot deployment application (8KiB bootloader)  --->
    Clock Reference (8 MHz crystal)  --->
    Communication interface (CAN bus (on PD0/PD1))  --->
    Application start offset (8KiB offset)  --->
    (1000000) CAN bus speed
    ()  GPIO pins to set on bootloader entry
    [*] Support bootloader entry on rapid double click of reset button
    [ ] Enable bootloader entry on button (or gpio) state
    [ ] Enable Status LED
```
5. `make clean && make`
6. Use the command to write CanBoot into the Manta
```
sudo dfu-util -a 0 -D ~/CanBoot/out/canboot.bin --dfuse-address 0x08000000:force:mass-erase -d 0483:df11
```

7. Go to your Klipper directory `cd ~/klipper`
8. Configure our new Klipper firmware for the Manta M5P `make menuconfig`

```
[*] Enable extra low-level configuration options
    Micro-controller Architecture (STMicroelectronics STM32)  --->
    Processor model (STM32G0B1)  --->
    Bootloader offset (8KiB bootloader)  --->
    Clock Reference (8 MHz crystal)  --->
    Communication interface (USB to CAN bus bridge (USB on PA11/PA12))  --->
    CAN bus interface (CAN bus (on PD0/PD1))  --->
    USB ids  --->
(1000000) CAN bus speed
()  GPIO pins to set at micro-controller startup
```
9. Build the klipper firmware `make clean && make`
10. Put the Manta M5P into DFU mode. Press and hold boot, then press and release the reset button, release the boot button. (sometimes simply double-clicking the reset button works too)
11. On your pi, type `lsusb`
12. You should see something like this. (if you don't check that you did exactly what is written in step 9)
```
    Bus 001 Device 011: ID 0483:df11 STMicroelectronics STM Device in DFU Mode
                                                                      ^^^^^^^^  important bit
```

13. Use this command to write klipper into the Manta
```
sudo dfu-util -a 0 -d 0483:df11 --dfuse-address 0x08002000:force:leave -D ~/klipper/out/klipper.bin
```

14. Set up the CAN Network by pasting this into your command line:
```
cat <<MEOW > /etc/network/interfaces.d/can0
auto can0
iface can0 can static
 bitrate 1000000
 up ifconfig $IFACE txqueuelen 1024
MEOW
```

15. Reboot the Raspberry PI and Manta and everything. You can do this by switching the power off and switching it back on again.
16. Reset your session/log back into your Raspberry PI
17. Type `ifconfig | grep can0` and check that there is something like this:
```
can0     Link encap:UNSPEC HWaddr 00-00-00-00-00-00...
```
The only thing important is you see it reply with a line that starts with `can0`.

17. If you see that then run the following command to query the UUIDs:
```
~/CanBoot/scripts/flash_can.py -i can0 -q
```

18. You should see only one UUIDs come up. If you see two, disconnect your EBB36 and try again.
```
Resetting all bootloader node IDs...
Checking for canboot nodes...
Detected UUID: abcdef123456, Application: Klipper
Query Complete
```
 
19. Write down the UUID, remember to note that this is the UUID of your Manta. You will need it later.

21. Plug in your EBB36, power cycle everything.
22. Run this script again 
```
~/CanBoot/scripts/flash_can.py -i can0 -q
```
22. You should get something like this:
```
Resetting all bootloader node IDs...
Checking for canboot nodes...
Detected UUID: abcdef123456, Application: Klipper
Detected UUID: fedcba654321, Application: Katapult
Query Complete
```

23. Write down the new EBB36/42 UUID. This is your toolhead UUID

25. Go to https://github.com/maz0r/klipper_canbus/tree/main/toolhead and find the toolhead and use those instructions to flash your toolhead board.

26. Once you are all done run this script again: 
```
~/CanBoot/scripts/flash_can.py -i can0 -q
```

27. Both UUIDs now should say Klipper
```
Resetting all bootloader node IDs...
Checking for canboot nodes...
Detected UUID: abcdef123456, Application: Klipper
Detected UUID: fedcba654321, Application: Klipper
Query Complete
```
28. If all this works, proceed to setting up your printer.cfg. Take the example printer.cfg of your printer and your toolhead board, but find the `[mcu]` and `[mcu <whatever>]` to modify  as shown in the printer.cfg section below:

## printer.cfg

```
[mcu]
canbus_uuid: <THE UUID YOU GOT IN STEP 19 ABOVE>
canbus_interface: can0

[mcu toolhead]
canbus_uuid: <THE UUID YOU GOT IN STEP 23 ABOVE>
canbus_interface: can0
```

## Aside

Vendor github is located here: https://github.com/bigtreetech/Manta-M5P/tree/master
Plagiarized from
- https://gist.github.com/fredrikasberg/c14f08eb8617bf8981f77dbc01b00602
- https://github.com/bigtreetech/Manta-M5P/issues/3
