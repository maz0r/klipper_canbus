# Canable & Clones

## **PI Setup**

` sudo nano /etc/network/interfaces.d/can0 `

```bash
allow-hotplug can0
iface can0 can static
 bitrate 500000
 up ifconfig $IFACE txqueuelen 256
 pre-up ip link set can0 type can bitrate 500000
 pre-up ip link set can0 txqueuelen 256
 ```

and press <kbd>Ctrl</kbd>+<kbd>X</kbd> to save.

you can now reboot the pi with ` sudo reboot `



## Test the network

Once the pi has rebooted you can run the `ip -s link show can0` command to check your network status.

You should see a line like the below in the results.
The key thing to note is that the network is **UP** for now.

![../images/iplink.png](../images/iplink.png)



## Can2USB firmware for Canable/U2C/UTOC boards

Optional (but may fix issues if your network doesnt start up)

You can flash candlelight firmware on many of the common boards (UTOC/U2C/Canable) with the following instructions

[./candlelight_fw.md](candlelight_fw.md)



### Suggested troubleshooting

1. If nothing shows up, try completely powering off printer and restarting it
2. Check that the toolboard is also flashed to 500k instead of 250k .




#### references

https://www.klipper3d.org/CANBUS.html
https://www.waveshare.com/wiki/RS485_CAN_HAT

### [Return to Main](../index.md)
