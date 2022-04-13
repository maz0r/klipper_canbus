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

## Initial Setup

Canbus wiring

![](images/canbus_wiring.svg)



## RS485 SPECIFIC

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

### Flashing the MCU



### Validation

PI W2 - BTT PICO - UART - MKS CANABLE PRO - HUVUD 0.61

PI 4B - BTT PICO - USB - Waveshare RS485 CAN HAT

?? can-utils

