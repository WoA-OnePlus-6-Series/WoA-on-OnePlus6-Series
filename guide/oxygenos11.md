<img align="top" src="https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/blob/main/OP6xT.png" width="500" alt="Windows 11 running on fajita/enchilada">

# OxygenOS 11 firmware flash ZIPs

## Requirements
- A OnePlus 6 or 6T with TWRP installed

- Device must have Slot A as active slot.

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [OnePlus USB Drivers](https://drive.google.com/file/d/1L7EZGx5mgeQYXO19Vsp9FWu9GXhF45Qs/view)
  
- [TWRP](https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/releases/tag/Stock-TWRP)

## Select your device
- [OnePlus 6T](https://oxygenos.oneplus.net/OnePlus6TOxygen_34.J.62_OTA_0620_all_2111252336_f6eda340d7af4e3e.zip)
- [OnePlus 6](https://oxygenos.oneplus.net/OnePlus6Oxygen_22.J.62_OTA_0620_all_2111252336_287bcb1636d743d3.zip)

## Installation
To install OxygenOS 11, download the ZIP, then you sideload or push it with adb.

### Pushing with ADB (PC Required)
First set your slot to B. Go to "Reboot" and tap on Slot B.
Then, check if your device is available.
```cmd
adb devices
```
If any device is there, you can push the zip to your device.
```cmd
 adb push path/to/oxygenos11.zip /sdcard
```
After this, go to main menu of TWRP and go to "Install". Tap on the ZIP and flash it

### Sideloading (PC Required)
Boot TWRP, Set slot to B, then go to "Advanced" and click on "ADB Sideload". The device should be in ADB now.
```cmd
adb sideload path/to/oxygenos11.zip
```

### Installing without a PC
Download the correct OxygenOS ZIP for your device. Place it in /sdcard.

Reboot to recovery.

After that, go to "Reboot" menu and choose Slot B.

Go back to the main menu.

Go to "Install" and go to /sdcard. There should be your OxygenOS ZIP.

Flash the ZIP and reboot your device.


