# A board level "hello world"

This section describes how quick start with D on the BBB.

## Get an official BBB Debian image onto the Micro SD card

get latest official BBB debian image with GUI (LXQT) or without GUI (IoT), here with

    wget https://debian.beagleboard.org/images/bone-debian-9.1-lxqt-armhf-2017-08-24-4gb.img.xz

verify sha256sum

    sha256sum bone-debian-9.1-lxqt-armhf-2017-08-24-4gb.img.xz

install tool to unpack .img.xz to .img

    sudo apt-get install xz-utils

plug the sd card (sd card adapter with the micro sd card) into the sd card slot and find the device

    ls /dev/mmc*

... should display something like

    /dev/mmcblk0  /dev/mmcblk0p1

change to root

    sudo su

copy the image onto the micro sd card

    xz -cd bone-debian-9.1-lxqt-armhf-2017-08-24-4gb.img.xz > /dev/mmcblk0

install tool to reload partition table

    sudo apt-get install parted

reload the partition table on the micro sd card

    partprobe /dev/mmcblk0

verify that a partition exists on the micro sd card

    ls -al /dev/mmcblk0*

... should show something like

    brw-rw---- 1 root disk 179, 0 Aug 31 18:07 /dev/mmcblk0
    brw-rw---- 1 root disk 179, 1 Aug 31 18:02 /dev/mmcblk0p1

create mount directory for the BBB image

    mkdir /media/bbb

mount the image and verify the content

    mount /dev/mmcblk0p1 /media/bbb
    ll

... should show something like

    drwxr-xr-x 21 root root  4096 Aug 24 21:20 ./
    drwxr-xr-x  4 root root  4096 Aug 31 18:14 ../
    -rw-r--r--  1 root root  1359 Aug 24 21:42 bbb-uEnv.txt
    drwxr-xr-x  2 root root  4096 Aug 24 21:00 bin/
    drwxr-xr-x  4 root root  4096 Aug 24 21:42 boot/
    (etc.)

unmount the micro sd card

    umount -l /dev/mmcblk0p1

[BeagleBoard website - latest images](http://beagleboard.org/latest-images)

[armhf.com - Getting Started with an Ubuntu or Debian .img.xz File](http://www.armhf.com/getting-started-with-ubuntu-img-file/)

## Hardware setup

connect BBB connector "USB" via microUSB-to-USB cable to a powered USB plug

connect a keyboard and a mouse to an USB port

connect the USB port to the BBB connector "USB HOST"

connect connector "HDMI" via microHDMI-to-HDMI cable to a screen

put the microSD card into BBB connector "microSD Card"

poweron

(no login required, default `username@hostname`: `debian@beaglebone` with password `temppwd`)

[BeagleBone website - Getting started](http://beagleboard.org/getting-started)

## Basic configuration

verify the network connection (eethernet cable connected to router)

    ping google.com

open "QTerminal"

update package listings

    sudo apt-get update

change keyboard layout (requires `sudo reboot`)

    sudo dpkg-reconfigure keyboard-configuration

## Install Cape Manager

figure out latest kernel

    apt-cache search linux-image

install the latest kernel (requires `sudo reboot`)

    sudo apt-get install linux-image-4.9.46-bone7

verify the cape manager directory

    ls /sys/devices/platform/bone_capemgr/

... should list something like

    baseboard  driver  driver_override  modalias  of_node  power  slots  subsystem  uevent

(device tree overlays are available from the [Robert C. Nelson's overlay repo](https://github.com/RobertCNelson/bb.org-overlays))

[thin-printer.com - Cape Manager is back baby!](https://www.thing-printer.com/cape-manager-is-back-baby/)

(Exploring BeagleBone, p. 222)

## Install D tools

install gdc:

```
sudo apt-get install gdc

```

check gdc version:

```
gdc --version

```

create `hello.d`...

```
nano hello.d

```

... with the following content:

```
import std.stdio;
void main()
{
   writeln("Hello D on BBB");
}

```

compile `hello.d` into the executable `hello`:

```
gdc hello.d -o hello

```

make the `hello` executable:

```
chmod +x hello

```

run `hello`:

```
./hello
Hello D on BBB

```

## Debugging with a serial-to-USB cable

If something goes wrong consider to connect a serial-to-USB cable to the BBB \(cable "GND" to BBB connector "J1" pin 1, cable "TX" to BBB connector "J1" pin 4, cable "RX" to BBB connector "J1" pin 5\).

install minicom or an equivalent `sudo apt-get install minicom`

start the serial console `sudo minicom -b 115200 -D /dev/ttyUSB0`

