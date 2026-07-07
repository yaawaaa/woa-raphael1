# Installing Linux on your device

### Prerequisites
- [Ubuntu Image](https://sourceforge.net/projects/linux-raphael/files/)
  
### Flashing the Ubuntu Rootfs
> [!NOTE]
> Make sure your device is in TWRP mode for this step.

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
Before finalizing, these files should be in the asset directory for your triple-boot script:
   - **boot_android.img** `(Your Android custom ROM kernel)`
   - **dtbo_android.img** `(Your Android custom ROM dtbo)`
   - **uefi_windows.img** `(The EDK2 UEFI boot file for Windows)`
   - **u-boot_ubuntu.img** `(Voxelsy's u-boot.img file renamed)`
   - **kernel_ubuntu.img** `(Voxelsy's xiaomi-k20pro-boot.img file renamed)`

## [Next step: Booting Linux](booting-linux.md)













































