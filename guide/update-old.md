<img align="right" src="https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/blob/main/enchilada.png" width="350" alt="Windows 11 running on fajita/enchilada">

# Running Windows on the OnePlus 6 / 6T

## Updating drivers (old method)

### Prerequisites
- [Drivers](https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/releases/tag/Drivers)
  
- [UEFI image](https://github.com/WoA-OnePlus-6-Series/WoA-on-OnePlus6-Series/releases/tag/UEFI)

### Boot to the UEFI
> Replace `path\to\devicename-uefi.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\devicename-uefi.img
```

#### Enabling mass storage mode
> Once booted into the UEFI, use the volume buttons to navigate the menu and the power button to confirm
- Select **UEFI Boot Menu**.
- Select **USB Attached SCSI (UAS) Storage**.
- Press the **power** button twice to confirm.

### Diskpart
```cmd
diskpart
```

#### Finding your phone
> This will list all connected disks
```cmd
lis dis
```

#### Selecting your phone
> Replace $ with the actual number of your phone (it should be the last one)
```cmd
sel dis $
```

#### Listing your phone's partitions
> This will list your device's partitions
```cmd
lis par
```

#### Selecting the Windows partition
> Replace $ with the partition number of Windows (should be 23)
```cmd
sel par $
```

#### Add letter to Windows
```cmd
assign letter x
```

#### Exit diskpart
```cmd
exit
```

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINONEPLUS** (which should be **X**), then press enter

#### Boot back into Windows
> Reboot your device to boot back into Windows. If this boots you to Android, reflash the UEFI image through fastboot or by using the WOA Helper app

## Finished!















