# An emulator level "hello world"

## Creating a Debian base system

create directory for BB root:

    sudo mkdir /BBroot

install debootstrap (Debian bootstrap) which allows to install a Debian base system into a subdirectory of a Debian based system (e.g. Ubuntu):

    sudo apt-get install debootstrap

install a Debian 9.1 (aka "Strech") root file system for ARM hard floats (arm-hf) from the Debian sources `http://ftp.us.debian.org/debian/dists/` into `/BBroot` (if one wants to use a BB board later it can be reasonable to choose the debian version w.r.t. supported Debian version images for the BB, see "board level hello D on BB"):

    sudo debootstrap --foreign --verbose --arch=armhf stretch /BBchroot http://ftp.us.debian.org/debian

check the root file system:

    ll /BBchroot

... should look like this:

    insgesamt 68
    drwxr-xr-x 17 root root 4096 Jan 29  2017 ./
    drwxr-xr-x 25 root root 4096 Sep  7 22:22 ../
    drwxr-xr-x  2 root root 4096 Mär 22 10:43 bin/
    drwxr-xr-x  2 root root 4096 Jul 13 15:04 boot/
    drwxr-xr-x  2 root root 4096 Sep  7 22:55 debootstrap/
    drwxr-xr-x  4 root root 4096 Sep  7 22:55 dev/
    drwxr-xr-x 26 root root 4096 Sep  7 22:55 etc/
    drwxr-xr-x  2 root root 4096 Jul 13 15:04 home/
    drwxr-xr-x  7 root root 4096 Jan 29  2017 lib/
    drwxr-xr-x  2 root root 4096 Jul 13 15:04 proc/
    drwx------  2 root root 4096 Jul 13 15:04 root/
    drwxr-xr-x  2 root root 4096 Jul 13 15:04 run/
    drwxr-xr-x  2 root root 4096 Sep  7 22:55 sbin/
    drwxr-xr-x  2 root root 4096 Jul 13 15:04 sys/
    drwxrwxrwt  2 root root 4096 Jul 13 15:04 tmp/
    drwxr-xr-x  9 root root 4096 Jan 29  2017 usr/
    drwxr-xr-x 11 root root 4096 Mai 27 17:44 var/

trying executing a binary `mkdir`...:

    ./mkdir

... will fail:

    /lib/ld-linux-armhf.so.3: No such file or directory

so we need to emulate the ARM `armhf` architecture on our `x86_64` (`uname -m`)

EBB, p. 257

## Emulation of the ARM architecture

install `qemu` (if required `sudo apt-get update` before)

    sudo apt-get install qemu-user-static

copy the statically compiled emulator into the change root directory (once executed `chroot` command no access to files outside
BBchroot directory including dynamic libraries due to "chroot jail"):

    cd /usr/bin
    sudo cp qemu-arm-static /BBchroot/usr/bin/

enter BBchroot (exit it with `exit`):

    sudo chroot /BBchroot/

check the architecture:

    I have no name!@e330:/# uname -a

... should show something like:

    Linux e330 4.4.0-93-generic #116-Ubuntu SMP Fri Aug 11 21:17:51 UTC 2017 armv7l GNU/Linux

complete the complete the debootstrap process with the second stage (installation of core packages,
unpacking and configuration of required packages, unpacking of base system):

    cd debootstrap/
    ./debootstrap --second‐stage

after quit a while you should see something like:

    I: Base system installed successfully.

set root password:

    passwd

EBB, p. 258
