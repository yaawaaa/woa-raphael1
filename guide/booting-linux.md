# Triple booting on the Xiaomi Mi 9T Pro / Redmi K20 Pro

## Booting Linux

### Prerequisites
- [Modified TWRP](https://github.com/new-WoA-Raphael/woa-raphael/releases/download/Files/modded-twrp-raphael.img)
  or
- An OrangeFox recovery that has parted
  
- [triboot script]()

- [Shortcut for Ubuntu]()

- [Shortcut for OrangeFox]()


### Boot into the recovery
Push the triboot.sh script to `/sdcard/` and run this command:
```cmd
sh /sdcard/triboot.sh ubuntu
```
It should boot you to Ubuntu. DON'T BOOT BACK TO ANDROID YET!!!

### Making the required files to switch os:
1. Create the local assets directory inside your Ubuntu Alacritty terminal:
> This should create a `Triboot_Assets` folder inside of the **Home** directory of Ubuntu
```cmd
mkdir -p ~/Triboot_Assets
```

2. Move the files that we copied earlier inside the /sdcard/Triboot_Assets folder into the Ubuntu **Triboot_Assets** folder that we just created.
`I don't know how to copy the files from the device itself so you need a pc or a cloud service to upload the file for this step`

### Switching OS'es Directly Inside Ubuntu
1. While in Ubuntu, connect to Wi-Fi, open your Alacritty terminal, and install the layout tool directly into the Linux environment:
> When it asks for a password, type: `1234`
```cmd
sudo apt update && sudo apt install parted -y
```
2. Copy the Scripts
Copy your **triboot.sh** and **shortcutsforubuntu.sh** script into your **Ubuntu home directory** folder so it is always native to the operating system.
`I don't know how to copy the scripts from the device onto ubuntu so you need a pc or a cloud service to upload the file for this step`
3. Booting to Android
If you are done using Linux and want to switch back to Android, just open Alacritty and run:
```cmd
sudo bash ~/shortcutsforubuntu.sh
```
This is a ONE TIME STEP and it will create an Android and Windows shortcut/application that you could access in the app launcher of Ubuntu.

### Switching Operating Systems
You are not locked into one OS. You can easily switch between your installed systems (Ubuntu, Windows, or Android) by using the shortcuts



### Diskpart
> [!WARNING]
> DO NOT ERASE, CREATE OR OTHERWISE MODIFY ANY PARTITION WHILE IN DISKPART!!!! THIS CAN ERASE ALL OF YOUR UFS OR PREVENT YOU FROM BOOTING TO FASTBOOT!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for flashing it with [EDL](edl.md), which will erase all your data)

```cmd
diskpart
```

#### Select the Windows volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **WINRAPHAEL**
```diskpart
select volume $
```

#### Assign the letter X
```diskpart
assign letter x
```

#### Select the ESP volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **ESPRAPHAEL**
```diskpart
select volume $
```

#### Assign the letter Y
```diskpart
assign letter y
```

#### Exit diskpart
```diskpart
exit
```

### Installing Windows
> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim or 22631.2861.XXXXXXX.esd)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Copying your boot.img into Windows
- Drag and drop the **rooted_boot.img** from the **platform-tools** folder into the **WINRAPHAEL** disk in Windows Explorer, then rename it to **boot.img**.

### Installing Drivers
- Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINRAPHAEL** (which should be **X**), then press enter

#### Create Windows bootloader files
> If any error shows up, such as "Failure when attempting to copy boot files", open `diskpart` again and assign any new letter to **ESPRAPHAEL**, then replace the letter `Y` in the next command with the letter that you just added.
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Remove the drive letter for ESP
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```

### Reboot to fastboot
```cmd
adb reboot bootloader
```

#### Boot into the UEFI
> Replace `path\to\raphael-uefi.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\raphael-uefi.img
```

### Reboot to Android
Your device should reboot by itself after +- 10 minutes of waiting, after which you will be booted into Android, for the last step.

## [Last step: Setting up dualboot](/guide/4-dualboot.md)




















