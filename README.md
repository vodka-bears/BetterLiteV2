# BetterLiteV2
The purpose of this project is to make Betafpv Lite Brushed V2 better. I decided to make it because I was kinda frustrated with its unfinished state. The main reason was that VTX frequency **in some branches of the board** is about 50 MHz ahead of the set frequency. And also I didn't like some words in OSD so I replaced them.
This repo contains binary files and flashers zipped in the root directory.
LiteSilverware repo: https://github.com/vodka-bears/LiteSilverware
LiteOSD repo: https://github.com/vodka-bears/LiteOSD
LiteVTX repo: https://github.com/vodka-bears/LiteVTX (only use if your board has a frequency issue)
efm8-arduino-programmer repo: https://github.com/vodka-bears/efm8-arduino-programmer
# Flashing
You can flash any of three components, interface between them hasn't been changed
## Flashing Silverware
To flash main MCU (STM32F042) with LiteSilverware you have to options. Either flash it with STLink or via USB in DFU mode. If you prefer STLink you probably know what you're doing. To flash with DFU yo need to follow these steps assuming you use 64-bit Windows (If you use some Linux you'll probably figure out from flash.bat):
* Download and unzip https://github.com/vodka-bears/BetterLiteV2/raw/main/dfu-flasher.zip
* If you want to backup the original FW proceed to the next step. Connect the board to USB without a battery attached.
* If nothing is detected in Windows or ypu want to backup original firmware, connect the board to USB without a battery attached and with jumper pins shorted with a screwdriver or something (see picture below)
* Realise that the flash memory on the MCU is probably erased and you can't fly until you reflash it if you didn't short pins.
* To backup go to dfu-util directory and run (in cmd) dfu-ultil.exe -A 0 -U backup.dfu
* To flash drag the lite_silverware.hex file onto flash.bat file in Explorer or use hex2dfu.exe and dfu-util.exe (you'll probably figure out)
* If the device detects in Windows but dfu-util doesn't detect the device, google "betaflight zadig" and do the same.

![Alt text](/docs/DFU.jpg?raw=true "Short this to enter DFU mode")
## Flashing OSD and VTX
To flash OSD and VTX you'll need some fine-soldering skills, python and some additional hardware. The hardware can be either an Arduino or C2 adapter from Ebay/Aliexpress. If you have a C2 Adapter please refer to its manual. If you have an Arduino, follow these steps:
* Install pyserial (pip install pyserial) (google pip if you don't know about this)
* Solder a wire to GND pin on the edge of the board and C2D and C2CK pins near the chip you want to flash (or both)
* If you have a C2 Adapter please refer to its manual. If you have an Arduino, flash it with prog.ino from here https://github.com/vodka-bears/efm8-arduino-programmer
* Connect C2D wire to D2 and C wire to D3 pins of an Arduino. Also connect a GND wire to GND pin.
* Plug the arduino to USB and check the com port name (something like COM6)
* Plug a charged battery to the board
* To backup the original firmware use `python read.py (com port name) (filename)`
* To flash use python `flash.py (com port name) (filename)`

![Alt text](/docs/c2.jpg?raw=true "Fine-soldering pins")
