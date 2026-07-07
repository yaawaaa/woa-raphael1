# Installing Linux on your device

### Prerequisites
- [Ubuntu Image](https://sourceforge.net/projects/linux-raphael/files/)

- [parted]()

- [OrangeFox Recovery]()
  
### Flashing the Ubuntu Rootfs
> [!NOTE]
> Make sure your device is in recovery mode for this step.

1. Move your chosen Ubuntu rootfs image file (like the Phosh 7.1 build) onto your phone's storage or a USB OTG drive. 
2. You can perform this step using the TWRP terminal directly on the phone, or by using an ADB terminal on your PC.

Execute the following command to flash the image file to the dedicated Linux partition:
> Replace `/path/to/your/rootfs.img` with the actual path of the image, such as /usb_otg/rootfs.img
```cmd
dd if=/path/to/your/rootfs.img of=/dev/block/by-name/ubuntu bs=4096
```
#### Preparing Boot Assets
Run these commands in your terminal to automatically set up and transfers the required files to the asset directory and back up your current Android kernel and DTBO:
1. Create the master assets folder
```cmd
mkdir -p /sdcard/Triboot_Assets
```

2. Back up and transfer the fresh(rooted) Android boot image 
```cmd
dd if=/dev/block/by-name/boot of=/sdcard/Triboot_Assets/boot_android.img bs=4096
```

3. Back up the fresh Android DTBO image (required for the script)
```cmd
dd if=/dev/block/by-name/dtbo of=/sdcard/Triboot_Assets/dtbo_android.img bs=4096
```

4. Push the custom U-Boot bootloader to the master assets folder
> Replace `/path/to/your/u-boot.img` with the actual path of the image
```cmd
./adb push "/path/to/your/u-boot.img" /sdcard/Triboot_Assets/u-boot_ubuntu.img
```

5. Push the Linux kernel to the master assets folder
> Replace `/path/to/your/xiaomi-k20pro-boot.img` with the actual path of the image
```cmd
./adb push "/path/to/your/xiaomi-k20pro-boot.img" /sdcard/Triboot_Assets/kernel_ubuntu.img
```

6. Push the UEFI to the master assets folder
> Replace `/path/to/your/uefi.img` with the actual path of the image but it will be most likely on `/sdcard/uefi.img`
```cmd
./adb push "/path/to/your/uefi.img" /sdcard/Triboot_Assets/uefi_windows.img
```
### Injecting Parted into OrangeFox
> [!WARNING]
> **Recovery Compatibility:** This injection method has only been tested and verified to work with the specific version of **OrangeFox Recovery** provided in this guide. Using other recovery environments may lead to unexpected behavior or boot failures. Use it with caution.
> You could use the recovery provided in the WOA guide but in my case it didn't boot when I messed up the automatic flashing.

To ensure your triple-boot script runs without dependency errors, you need to add the `parted` utility to your recovery environment.
1. Flash the OrangeFox recovery provided in this guide in fastboot
> Replace `/path/to/your/ofox.img` with the actual path of the image
```cmd
fastboot flash /path/to/your/ofox.img
```

2. Locate Parted on Your Computer
Download parted and Copy it into your `C:\adb\` folder.

3. Push Parted to Your Asset Vault
Reboot your phone into OrangeFox recovery, connect it to your PC, and run this command in PowerShell to send the binary over:
```cmd
./adb push parted /sdcard/Triboot_Assets/parted
```

4. Make Parted a Global System Command
Open the terminal inside OrangeFox (or run ./adb shell from your PC) and run these two lines to copy parted into the recovery's active system path and grant it execution permissions:
```cmd
cp /sdcard/Triboot_Assets/parted /sbin/parted
chmod +x /sbin/parted
```

Before finalizing, these files should be in the asset directory for your triple-boot script:
   - **boot_android.img** `(Your Android custom ROM kernel)`
   - **dtbo_android.img** `(Your Android custom ROM dtbo)`
   - **uefi_windows.img** `(The EDK2 UEFI boot file for Windows)`
   - **u-boot_ubuntu.img** `(Voxelsy's u-boot.img file renamed)`
   - **kernel_ubuntu.img** `(Voxelsy's xiaomi-k20pro-boot.img file renamed)`
   - **parted** `(a partitioner without an extension)`
**I recommend copying these files somewhere like in your pc or in cloud because we are gonna need all of these files in Ubuntu**

## [Next step: Booting Linux](booting-linux.md)













































