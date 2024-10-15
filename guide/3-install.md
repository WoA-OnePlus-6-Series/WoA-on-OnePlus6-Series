<img align="right" src="https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/blob/main/OP6xT.png" width="350" alt="Windows 11 running on fajita/enchilada">

# Running Windows on the OnePlus 6 / 6T

## Installing Windows

### Prerequisites
- [Windows on ARM image](https://arkt-7.github.io/woawin/)
  
- [Drivers](https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/releases/tag/Drivers)
  
- [UEFI image](https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/releases/tag/UEFI)

- [Modded TWRP](https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/releases/tag/Recovery)

### Boot to TWRP
> Replace `path\to\twrp-op6xt.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\twrp-op6xt.img
```

#### Execute the msc script
> If it asks you to run it once again, do so
```cmd
adb shell msc
```

### Diskpart
> [!WARNING]
> DO NOT ERASE ANY PARTITION WHILE IN DISKPART!!!! THIS WILL ERASE ALL OF YOUR UFS!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for flashing it with EDL, which will wipe your data)
```cmd
diskpart
```

#### Select the Windows volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **WINONEPLUS**
```diskpart
select volume $
```

#### Assign the letter X
```diskpart
assign letter x
```

#### Select the ESP volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **ESPONEPLUS**
```diskpart
select volume $
```

#### Assign the letter Y
```diskpart
assign letter y
```

#### Exit diskpart
```cmd
exit
```

### Installing Windows
> [!Warning]
> DO NOT USE 24H2!!!

> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim or 22631.2861.XXXXXXX.esd)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Copying your boot.img into Windows
- Drag and drop the **rooted_boot.img** from the **platform-tools** folder into the **WINONEPLUS** disk in Windows Explorer, then rename it to **boot.img**.

### Installing Drivers
- Unpack the driver archive, then open the `DEVICENAMEFirstboot.cmd` file (if an error shows up, run `DEVICENAMEFirstbootFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINONEPLUS** (which should be **X**), then press enter

> [!IMPORTANT]
> After you finish installing the drivers, copy the drivers archive into the root of **WINONEPLUS** with Windows Explorer. After you boot into Windows for the first time, extract it, then open the `OnlineUpdater.cmd` file to update to the correct drivers.

#### Create Windows bootloader files
> If any error shows up, such as "Failure when initializing library system volume.", open `diskpart` again and assign any new letter to **ESPONEPLUS**, then replace the letter `Y` in the next commands with the letter that you just added.
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Enabling test signing
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Disabling recovery
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Disabling integrity checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Remove the drive letter for ESP
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```

### Reboot to fastboot
> Hold **volume down** + **power** to force reboot your phone into fastboot mode

#### Boot into the UEFI
> Replace `path\to\devicename-uefi.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\devicename-uefi.img
```

### WARNING
> [!Warning]
> NEVER USE SLOT SWITCH IN UEFI! IT BRICKS YOUR PHONE

### Reboot to Android
Your device should reboot by itself after +- 10 minutes of waiting, after which you will be booted into Android, for the last step.

## [Last step: Setting up dualboot](/guide/4-dualboot.md)

















