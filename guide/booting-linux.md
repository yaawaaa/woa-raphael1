# Triple booting on the Xiaomi Mi 9T Pro / Redmi K20 Pro

## Booting Linux

### Prerequisites
- [Modified TWRP](https://github.com/new-WoA-Raphael/woa-raphael/releases/download/Files/modded-twrp-raphael.img)
  or
- An OrangeFox recovery that has parted
  
- [triboot script](https://github.com/yaawaaa/woa-raphael1/releases/download/scripts/triboot.sh)

- [Shortcut for Ubuntu](https://github.com/yaawaaa/woa-raphael1/releases/download/scripts/shortcutsforubuntu.sh)

- [Shortcut for OrangeFox](https://github.com/yaawaaa/woa-raphael1/releases/download/scripts/ofoxshortcuts.sh)

- [Termux](https://f-droid.org/en/packages/com.termux/)

- [Termux:Widget](https://f-droid.org/en/packages/com.termux.widget/)

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

### Switching OS'es Directly Inside Android
Boot back to Android using the shortcuts if they work, if they don't go to [Troubleshooting](troubleshooting.md) page. Root should be on for these steps.
1. Install **Termux** and **Termux:Widget** and run this command:
```cmd
mkdir -p ~/.shortcuts/tasks
```
2. Create the Ubuntu Boot Button
Run this single line in Termux to build your automated Ubuntu launcher script:
```cmd
echo -e '#!/data/data/com.termux/files/usr/bin/sh\nsu -c "sh /sdcard/triboot.sh ubuntu"' > ~/.shortcuts/tasks/Boot_Ubuntu.sh
```
(Optional) Create the Windows Boot Button
```cmd
echo -e '#!/data/data/com.termux/files/usr/bin/sh\nsu -c "sh /sdcard/triboot.sh windows"' > ~/.shortcuts/tasks/Boot_Windows.sh
```
4. Grant Executive Permissions
Tell the Android system these scripts are allowed to execute automatically:
```cmd
chmod +x ~/.shortcuts/tasks/*
```
5. Add the Boot Buttons to Your Home Screen
Long-press on an empty space on your Android home screen and select **Widgets**. Scroll down to **Termux**, select the **Termux:Widget** option, and drag it onto your screen. A menu will appear displaying your `Boot_Ubuntu.sh` and `Boot_Windows.sh` scripts, which you can now tap to launch.

### Switching OS'es Directly Inside Recovery
1. While in Android, open termux and run this command:
```cmd
pkg install zip -y
```
2. After running it, copy **ofoxshortcuts.sh** to `/sdcard/` and run this command:
```cmd
sudo bash /sdcard/ofoxshortcuts.sh
```
3. You should see 3 .zip files that you could flash if you are in OrangeFox Recovery.


### Switching Operating Systems
You are not locked into one OS. You can easily switch between your installed systems (Ubuntu, Windows, or Android) by using the shortcuts



## Finished!




















