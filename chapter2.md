# Hardware interfacing

This section describes how to interact with the hardware interfaces of the BBB.

## LEDs

### Background

To beeing able to write a script or a class to interact with the LEDs one needs to understand how one interacts in general
with the LEDs via character device drivers e.g. over the command line.

disable heartbeat flashing of led "USER LEDS D2 0":

    cd /sys/class/leds/beaglebone:green:usr0
    echo none > trigger

enable led "USER LEDs D2 0":

    echo 1 > brightness

disable led "USER LEDs D2 0":

    echo 0 > brightness

flash led "USER LEDs D2 0":

    echo timer > trigger

restore heartbeat flashing of led "USER LEDS D2 0":

    echo heartbeat > trigger

[Beaglebone: Controlling the on-board LEDs using C++](http://derekmolloy.ie/beaglebone-controlling-the-on-board-leds-using-c/)

### Script

To interface the LEDs of the BBB via the character device drivers with a D script refer to the
[LED scripts in the "Exploring BeagleBone" companion repository](https://github.com/derekmolloy/exploringBB/tree/master/chp05/dLED).
