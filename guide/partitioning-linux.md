# Triple booting on the Xiaomi Mi 9T Pro / Redmi K20 Pro

## Partitioning your device

### Prerequisites
- A functioning brain (most important of all)
  
- Unlocked bootloader
  
- Preferably the latest firmware installed
  
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Modified TWRP](https://github.com/new-WoA-Raphael/woa-raphael/releases/download/Files/modded-twrp-raphael.img)

### Notes
> [!WARNING]  
> All your data will be erased! Back up now if needed.
> 
> Do not run the same command twice.
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woaraphael).
> 
> Do not run all commands at once, execute them in order!

> [!IMPORTANT]
> Make sure you use the MODDED Recovery throughout this whole tutorial as we provide tools to help aid this installation process and make it as easy as possible for you.
> 
> If you don't use it and you face any errors, consider it your fault and consider yourself alone if you try asking for support as you have deferred from the main guide.
> **Plan Ahead for Triple Booting:** If you intend to install Linux as the final step, you must reserve unallocated space on your disk during the partitioning phase. 
> Please ensure your partition layout leaves enough free space for Ubuntu (recommended: at least 20-30GB) before proceeding with the Windows installation guide below.

### Installing Windows
1. Follow the steps in the [official Windows guide](https://github.com/new-WoA-Raphael/woa-raphael/blob/main/guide/1-partition.md).
2. **Crucial:** When the guide asks you to allocate space, **you must reserve an additional 20-30GB of unallocated space** at the end of the drive for your Linux partition.
3. You can install Windows first and then lastly Linux.
4. After finishing the Windows installation part of that guide, return here to proceed with Linux.

#### Creating Linux partition
> Replace the end value you want **ubuntu** to have. For example, if your last partition ends at **50GB** and you want 20GB for Linux, set your new partition end to **70GB**.
```cmd
mkpart ubuntu ext4 236GB 256GB
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

### Formatting Linux
> Reboot into the modded recovery, then run the command below.
```cmd
mke2fs -t ext4 /dev/block/by-name/ubuntu
``` 

## [Next step: Installing Linux](/guide/installing-linux.md)















