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

> [!Note]
> If your device is not detected in fastboot or recovery mode, you'll have to install USB drivers [using this guide](troubleshooting.md#device-is-not-recognized-in-fastboot-or-recovery)

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

### Partitioning your device
> There are two methods to partition your device. Please select the method you would like to use below. 

#### Method 1: Manual partitioning 

<details>
  <summary><strong>Click here for method 1</strong></summary> 

#### Opening a shell
```cmd
adb shell
```

### Preparing for partitioning
$${\color{lightblue}🟦 Note}$$
> If at any moment in parted you see an error prompting you to type "Yes/No" or "Ignore/Cancel", type `Yes` or `Ignore` depending on the situation to ignore the errors and continue.
>
> If you see any **udevadm** errors, you can ignore these as well.
```cmd
parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list
```cmd
print
``` 

#### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be **17**
```cmd
rm $
``` 

#### Recreating userdata
> Replace **6559MB** with the former start value of **userdata** which we just deleted
>
> Replace **40GB** with the end value you want **userdata** to have. In this example your available usable space in Android will be 40GB-6559MB = **33GB**
```cmd
mkpart userdata ext4 6559MB 40GB
``` 

#### Creating ESP partition
> Replace **40GB** with the end value of **userdata**
>
> Replace **40.3GB** with the value you used before, adding **0.3GB** to it
```cmd
mkpart esp fat32 40GB 40.3GB
``` 

#### Creating Windows partition
> Replace **40.3GB** with the end value of **esp**
```cmd
mkpart win ntfs 40.3GB -0MB
``` 

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be **18**
```cmd
set $ esp on
``` 

#### Exit parted
```cmd
quit
``` 

### Formatting data
- Format all data in TWRP, or Android will not boot.
- ( Go to Wipe > Format data > type yes ) 

#### Check if Android still starts
- Just restart the phone, and see if Android still works 

### Formatting Windows and ESP drives
> Reboot into the modded recovery, then run the below two commands
```cmd
adb shell mkfs.ntfs -f /dev/block/by-name/win -L WINONEPLUS
``` 

```cmd
adb shell mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESPONEPLUS
``` 

</details>

#### Method 2: Automatic partitioning 

<details>
  <summary><strong>Click here for method 2</strong></summary> 

### Run the partitioning script
> Replace **$** with the amount of storage you want Windows to have (do not add GB, just write the number)
> 
> If it asks you to run it once again, do so
```cmd
adb shell partition $
``` 

### Check if Android still starts
- Just restart the phone, and see if Android still works 

</details>

## [Next step: Rooting your phone](/guide/2-root.md)















