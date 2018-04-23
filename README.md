# Build_System

## Clone and Build for QEMU
Clone from GitHub and checkout the latest version.
```
$ git clone git://git.buildroot.net/buildroot
$ git checkout 2018.02
```
Use the qemu default configuration and build
```
$ cd buildroot
$ make qemu_arm_versatile_defconfig
$ make
```
Two new directories will be created, the bootloader, kernel and one or more root filesystem images will be in output/images/

## Start QEMU with the target
```
$ quemu-system-arm -M versatilepb -m 256 \
-kernel output/images/zImage \
-dtb output/images/versatile-pb.dtb \
-drive file=output/images/rootfs.ext2,if=scsi,format=raw \
-append "root=/dev/sda console=ttyAMA,115200" \
-serial stdio -net nic,model=rtl8139 -net user
```
## Build for Raspberry Pi 2 and Write SD Card
The detail information is the buildroot/board/raspberrypi2/readme.txt
``` 
$ make raspberrypi2_defconfig
$ make
$ sudo dd if=output/images/sdcard.img of=/dev/sdX
```
X is depend on the SD card. \
Buildroot uses a tool named genimage to create an image for SD card, that's why we just need to copy sdcard.img, not every images separately.
