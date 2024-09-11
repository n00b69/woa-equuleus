<img align="right" src="https://github.com/n00b69/woa-equuleus/blob/main/equuleus.png" width="350" alt="Windows 11 running on equuleus">

# Running Windows on the Xiaomi Mi 8 Pro

## Updating drivers

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Mass storage image](https://github.com/n00b69/woa-equuleus/releases/download/Files/msc.img)

- [UEFI image](https://github.com/n00b69/woa-equuleus/releases/tag/UEFI)

- [Drivers](https://github.com/n00b69/woa-equuleus/releases/tag/Drivers)
  
### Boot into the mass storage image
> Replace `path\to\msc.img` with the actual path of the image
```cmd
fastboot boot path\to\msc.img
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

### Diskpart
```cmd
diskpart
```

#### Select Windows volume
> Use `list volume` to find it, replace `$` with the actual number of **WINEQUULEUS**
```cmd
select volume $
```

#### Assign the letter X
```cmd
assign letter x
```

#### Exit diskpart
```cmd
exit
```

### Installing Drivers
> [!Note]
> This process will take +- 20 minutes. Do not worry, this is normal.

- Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINEQUULEUS** (which should be **X**), then press enter

#### Reboot your device
> Make sure to also change the UEFI image in Android, otherwise you may face a "blue screen of death" (BSoD) when booting Windows later.

## Finished!













