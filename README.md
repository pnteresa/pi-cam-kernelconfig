# pi-cam-kernelconfig
Raspberry Pi based webcam kernel config, for v4.1.15. This will compile the kernel in LZMA compression format, resulting in ~2.4MB (2.39 MB) in size.

Tugas Sysprog kelompok **The Agents**- other members (credits for GPIO and Bootscripts: Alvin, Anthony, Christian, Saga)

##Steps:

#####Clone toolchains:

<code>git clone https://github.com/raspberrypi/tools.git</code>

<code>git clone https://github.com/raspberrypi/linux.git</code>

#####Export path variable:
<code>
user@user-PC:~/raspberry-linux/linux$ > export CCPREFIX="/home/user/raspberry-linux/tools/arm-bcm2708/arm-bcm2708-linux-gnueabi/bin/arm-bcm2708-linux-gnueabi-"
</code>

#####Clean (if you have compiled before)
<code>
user@user -PC:~/raspberry-linux/linux$ > make mrproper
</code>

#####Copy the config file from this repo to linux folder as .config
<code>
user@user -PC:~/raspberry-linux/linux$ > cp this_file_config .config
</code>

#####Adjust the kernel:
<code>
user@user -PC:~/raspberry-linux/linux$ > make ARCH=arm CROSS_COMPILE=${CCPREFIX} menuconfig
</code>
Note: <code>menuconfig</code> may be changed with xconfig or oldconfig

#####Compile!
<code>
user@user -PC:~/raspberry-linux/linux$ > make ARCH=arm CROSS_COMPILE=${CCPREFIX} -k -j5
</code>
Note: change 5 in j5 with the number of your PC cores + 1

##Tips
- *Always* keep track with the changes! Documentation is very important as you might change many configurations
- You can see <code>lsmod</code> in your Pi to know the modules used (but not all are covered here)
- My big-nos in kernel (may be different than yours):
 - Natural Language Support (except codepage437, ASCII and UTF-8)
 - Bluetooth, Infrared, NFC
 - Filesystems (just leave ext4)
 - Sound
 - Joystick and friends
 - USB supports
 - Multimedia supports
 - Industrial IO support (drops 200KB, cmiiw)
 - Accelerometer and stuffs
 
##Notes
- By December '15, the latest keychain is v4.1.15 and this kernel uses v4.1.15 firmware. Make sure to change linux's git branch to 4.1.y
