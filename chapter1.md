# A board level "hello world"

This section describes how quick start with D on the BBB.

## Get an Ubuntu image onto the SD card

get a prebuilt Ubuntu image

```
wget https://rcn-ee.com/rootfs/2017-07-14/elinux/ubuntu-16.04.2-console-armhf-2017-07-14.tar.xz

```

verify the image:

```
sha256sum ubuntu-16.04.2-console-armhf-2017-07-14.tar.xz

```

unpack the image and `cd`:

```
tar xf ubuntu-16.04.2-console-armhf-2017-07-14.tar.xz
cd ubuntu-16.04.2-console-armhf-2017-07-14

```

put your microsd card into a sd card adapter, put the sdcard adapter into the laptops sdcard plug

get the device name \(`/dev/mmcblk0`\) of the sdcard

```
sudo ./setup_sdcard.sh --probe-mmc

```

install the image onto the sdcard \(for other boards replace `beaglebone` with: BeagleBoard Ax/Bx/Cx/Dx `omap3-beagle`, BeagleBoard xM `omap3-beagle-xm`, OMAP5432 uEVM `omap5-uevm`, BeagleBoard-X15 `am57xx-beagle-x15`\):

```
sudo ./setup_sdcard.sh --mmc /dev/mmcblk0 --dtb beaglebone

```

[BeagleBoard Ubuntu on eLinux](http://elinux.org/BeagleBoardUbuntu)

## BBB setup

connect BBB connector "USB" via microUSB-to-USB cable to a powered USB plug

connect a keyboard to BBB connector "USB HOST"

connect connector "HDMI" via microHDMI-to-HDMI cable to a screen

put the microSD card into BBB connector "microSD Card"

poweron

## Login into Ubuntu

poweron \(startup jobs take quite a while until login screen pops up\)

```
arm login: ubuntu
Password: temppwd

```

ready for D on BBB:

```
ubuntu@arm:~$

```

## Basic configuration

\(optional\) adjust keyboard layout \([english keyboard layout](https://en.wikipedia.org/wiki/British_and_American_keyboards#/media/File:KB_US-International.svg), german keyboard: `z` gets `y`\):

```
sudo loadkeys de

```

create a swap file \(required that `apt-get` and other stuff works correctly despite of BBB's little RAM\)

```
sudo mkdir -p /var/cache/swap/   
sudo dd if=/dev/zero of=/var/cache/swap/swapfile bs=1M count=1024
sudo chmod 0600 /var/cache/swap/swapfile 
sudo mkswap /var/cache/swap/swapfile
sudo swapon /var/cache/swap/swapfile 

```

use swap on every boot by adding `/var/cache/swap/swapfile none swap sw 0 0` to `/etc/fstab`:

```
sudo nano /etc/fstab

```

if the BBB is connected to a network with dhcp server running it should get an ip. in some cases it does not get an ip. execute `sudo ifdown eth0; sudo ifup eth0` as workaround. websites should be pingable with `ping google.com`.

update apt-get:

```
sudo apt-get update

```

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

