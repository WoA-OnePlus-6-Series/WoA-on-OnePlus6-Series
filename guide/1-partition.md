<img align="right" src="https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/blob/main/OP6xT.png" width="350" alt="Windows 11 running on fajita/enchilada">

# Running Windows on the OnePlus 6 / 6T

## Partitioning your device

### Prerequisites
- Unlocked bootloader

- [OxygenOS 11 Firmware](https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/blob/main/guide/oxygenos11.md)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [OnePlus USB Drivers](https://drive.google.com/file/d/1L7EZGx5mgeQYXO19Vsp9FWu9GXhF45Qs/view)
  
- [Modded TWRP](https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/releases/tag/Recovery)

### Notes
> [!WARNING]  
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/WinOnOP6).
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

### Opening CMD as an admin
> Download **platform-tools** and extract the folder somewhere, then open CMD as an **administrator**.
>
> It is recommended to keep this window open and use it throughout the entire guide.
> 
> Replace `path\to\platform-tools` with the actual path to the platform-tools folder, for example **C:\platform-tools**.
```cmd
cd path\to\platform-tools
```

> [!IMPORTANT]
> Make sure you use the MODDED Recovery throughout this whole tutorial as we provide tools to help aid this installation process and make it as easy as possible for you.
> 
> If you don't use it and you face any errors, consider it your fault and consider yourself alone if you try asking for support as you have deferred from the main guide.

#### Boot the modded recovery
> While in fastboot mode, replace `path\to\twrp.img` with the actual path of the image
```cmd
fastboot boot path\to\twrp.img
```

### Backing up important files
> This will back up **fsc**, **fsg**, **modemst1** and **modemst2** to the current path your CMD is opened in (for example **C:\platform-tools**). Confirm these files are actually there before proceeding.
> 
> Keep these backups in a safe place. If your device's software ever gets destroyed, you might need these backups or your phone could lose cellular capabilities.
>
> If you've got anything else you want to back up, do this now. Your Android data will be erased in the next steps.
```cmd
cmd /c "for %i in (fsg,fsc,modemst1,modemst2) do (adb shell dd if=/dev/block/by-name/%i of=/tmp/%i.bin & adb pull /tmp/%i.bin)"
```

#### Backing up your boot image
> This will back up your boot image in the current directory
```cmd
adb pull /dev/block/by-name/boot_a boot.img
```

### Partitioning guide
> If you have a 64GB OnePlus 6 or 6T, please contact us in our [Telegram Group](https://t.me/WinOnOP6)

### Run the partitioning script
> Replace **$** with the amount of storage you want Windows to have (do not add GB, just write the number)
> 
> If it asks you to run it once again, do so
```cmd
adb shell partition $
```
### Formatting data
- Format all data in TWRP, or Android will not boot.
- ( Go to Wipe > Format data > type yes )

### Check if Android still starts
- Just restart the phone, and see if Android still works

## [Next step: Rooting your phone](/guide/2-root.md)
















