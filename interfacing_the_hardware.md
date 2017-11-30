# Hardware interfacing

This section describes how to interact with the hardware interfaces of the BBB.

## Background

### Device Tree Overlays

Kernel patches for the BBB provide a "Cape Manager" which allows to load and
remove DTOs during runtime. This eases the hardware/software integration because
one does not need to recompile the flatened device tree. It is possible to load
DTOs right after boot which means one must not recompile the kernel at all.

TODO: The instructions of the Cape Manager how to apply the DTOs in
(Molloy 2015, p. 222) are outdated. Adjust generic instructions to current state.

## LEDs

### Background

To beeing able to write a script or a class to interact with the LEDs one needs
to understand how one interacts in general with the LEDs via character device
drivers e.g. over the command line.

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

## Analog Inputs

### Background

The analog-to-digital converter provides analog inputs to the `sysfs` which can be
read with D applications via the command line.

apply the device tree overlay "BB‐ADC":

    sudo sh -c "echo 'BB-ADC' > $SLOTS"

read analog input 0:

    cd /sys/bus/iio/devices/iio:device0
    cat in_voltage0_raw

... should shows some value between 0 and 4095 (dependent on the configuration of
  the ADC which has a resolution of 12‐bit ADCs, means 2^12 = 4,096):

    3831

### Script

To interface with analog inputs of the BBB refer to this
[script which reads an analog input](https://github.com/fkromer/exploringBB/blob/readldr/chp06/ADC/d/readLDR.d).
Consider (Molloy 2015, p. 228) for an application of the script with an external
light meter circuit connected to the BBB.
