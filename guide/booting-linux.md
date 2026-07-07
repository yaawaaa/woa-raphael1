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

### Switching OS'es Directly Inside Android
Boot back to Android using the shortcuts if they work, if they don't go to [Troubleshooting]() page.
### Switching Operating Systems
You are not locked into one OS. You can easily switch between your installed systems (Ubuntu, Windows, or Android) by using the shortcuts

## Finished!




















