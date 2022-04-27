# 3DMellow UTOC 1 & 3

## Troubleshooting

1. > My device doesnt have a name when I run `lsusb`
   
If your device id is `4d4c:5543` you have an early revision of the board intended for use with the Gemini boards, these boards ship with a firmware which is not recognised by Linux and will require manual flashing in order to resolve. [see utoc flashing](#flashing-utoc-firmware)


2. > I can see my `can0` network but when I connect my device to query the uuid there is no value returned.

    [Check Wiring]()

    [Check Firmware]()

    [Check Termination]()











## Flashing UTOC Firmware

[back to top](#3dmellow-utoc-1--3)

In order to flash the UTOC a jumper cap needs to be installed as indicated in the picture (for UTOC-1 I believe it's in the same place).

![UTOC Bootloader PIN](../images/utoc_flash.png)



[utc_firmware.bin](./firmware_files/utoc_firmware.bin) 