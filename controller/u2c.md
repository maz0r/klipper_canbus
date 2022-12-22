# Bigtreetech U2C 1 & 3

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


## Wiring Guide -- Coming Soon

## Termination Guide - Coming Soon

## Troubleshooting

1. > I can see my `can0` network but when I connect my device to query the uuid there is no value returned.

    [Check Wiring]()

    [Check Firmware]()

    [Check Termination]()


## Flashing U2C Firmware

In order to flash the U2C the `boot` and `reset` buttons need to be pressed and released after connecting he board (release `boot` last.

You can then **flash [candlelight_fw](./candlelight_fw.md)**



### [Return to Main](../index.md)