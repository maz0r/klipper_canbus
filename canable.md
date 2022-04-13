# Canable & Clones

## **PI Setup**

` sudo nano /etc/network/interfaces.d/can0 `

```bash
auto can0
iface can0 can static
 bitrate 250000
 up ifconfig $IFACE txqueuelen 256
 pre-up ip link set can0 type can bitrate 250000
 pre-up ip link set can0 txqueuelen 256
 ```

and press <kbd>Ctrl</kbd>+<kbd>X</kbd> to save.

you can now reboot the pi with ` sudo reboot `

### Suggested troubleshooting

1. If nothing shows up, try completely powering off printer and restarting it
2. Check that the toolboard is flashed to 250k instead of 500k to match the above.

#### references

https://www.klipper3d.org/CANBUS.html
https://www.waveshare.com/wiki/RS485_CAN_HAT

### [Return to Main](install.md)