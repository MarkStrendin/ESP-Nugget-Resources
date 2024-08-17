# ESPNuggets
Resources for programming WiFi Nuggets and USB Nuggets, because the official documentation is often not complete or accurate, and Chrome often fails to flash the devices properly every time.

This is not meant to be a replacement for the official documentation, this is merely information I've gathered myself to make working with these devices more straightforward.

# Official Resources
- https://nugget.dev
- https://usb.nugget.dev
- https://wifi.nugget.dev/

# Manually flashing
Retia LLC has build an amazing flashing tool on their website (https://nugget.dev), but I have found that it often doesn't properly flash the chip the first time, and it can get generally unlreliable the longer that Chrome is open. I suspect these are Chrome related issues, rather than issues with their site. The site also only works in Chrome (or presumably Microsoft Edge also), but some people (like Linux users) may not want to have Chrome installed.

You can manually flash using [Espressif's ESPTool](https://docs.espressif.com/projects/esptool/en/latest/esp32/installation.html), which is much more reliable because it doesn't involve a web browser in the middle of it.

## Installing ESPTool
 - Install Python, if its not already installed on your system
 - Install PIP, if it is not already installed on your system
 - Open a command line and type `pip install esptool`

## Putting the Nugget in flashing mode
### WiFi Nugget
Does not need to be put into flashing mode, just plug it in.

### USB Nugget
- If your USB nugget has a case, remove it from the case
- The smaller ESP board will have two buttons on it - press and hold the button labelled `0` (Not the one labeleld `RST`)
- While holding the button, plug the USB nugget into your computer via a USB cable.

## Flashing
```sh
esptool --port COMPORT write_flash 0x0000 FIRMWARE.bin
```
Example:
```sh
esptool --port COM6 write_flash 0x0000 v1.0-Nugget-Invader.bin
```

The `esptool` utility will automatically restart the device, so there is no need to cycle power after a flash.

## Obtaining official firmware bins from nugget.dev
Firmware files are linked below, but they may be updated on the server, and may become out of date in this repo. Here is how to download or find their URLs again.
 - Using Chrome go to https://nugget.dev
 - Plug your nugget into USB
 - Open Chrome's developer tools (Probably by pushing F12, but sometimes you need to find it in the menu instead)
 - In developer tools, select the "Network" tab
 - Press "Connect" and select the nugget from the pop-up list
 - The page will go to the firmware select page
 - Change the selected firmware, and you will see each time it downloads a .bin file
 - Right click the record for the .bin file in the network tab's connections list, and select "Open in new tab" to download

### Official firmware
#### WiFi Nugget
 - Deauth Detector - https://nugget.dev/js/binaries/DeauthDetector.bin
   - No user interaction
   - DEAUTH packets make happy cat face turn into a sad cat face
 - MicroPython - https://nugget.dev/js/binaries/micropython.bin
   - https://micropython.org/
 - Nugget Deauther - https://nugget.dev/js/binaries/NuggetDeauther.bin
   - Default firmware
   - DEAUTH Attack
 - Nugget DeAuther V3 - https://nugget.dev/js/binaries/esp8266_deauther_V3.bin
   - Advanced WiFi attack and detection features
   - No screen, serial control only

#### USB Nugget
 - USB Nugget - https://nugget.dev/js/binaries-usb/USBNugget.bin
   - Default firmware
 - Packet Monitor - https://nugget.dev/js/binaries-usb/PacketMonitor.bin
 - Circuit Python - https://nugget.dev/js/binaries-usb/CircuitPython.bin
   - https://circuitpython.org/
 - WLED - https://nugget.dev/js/binaries-usb/wled_flash_dump.bin


### Other non-official firmware
#### WiFi Nugget
 - https://github.com/DevKitty-io/Nugget-Invader
   - DEAUTH Attack
   - Packet Monitor (shows live data from detected packets)
   - Apparently abandoned, but still works
