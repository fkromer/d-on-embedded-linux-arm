# Remote control

## Introduction into networking

A typical private network looks like this...:

![Interface the BB via Ethernet, host WLAN](diagrams/BB_remote_access.png)

...or like this (because the BB has no wireless network adapter included):

![Interface the BB via Ethernet, host via Ethernet](diagrams/BB_remote_access_host_wireless.png)

on the host get the ip address of the host itself with usually something like
`eth0` as interface if using LAN and something like `wlp2s0` as interface if using
WLAN:

    ifconfig eth0 | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}'

on the host get the ip address of the router (should show something like `192.168.178.20`):

    netstat -nr | awk '$1 == "0.0.0.0"{print$2}'

on the host scan the network to get the ip address of the connected devices including the BB:

    nmap -sP 192.168.178.1/24

...should show something like:

    ...
    Nmap scan report for beaglebone.fritz.box (192.168.178.5)
    Host is up (0.78s latency).
    ...

Configure the router to assign/use always the same ip address (static ip) for the
BB and the host pc. The procedure depends on the actual router. Usually the router
provides a web gui which can be accessed by visiting the routers ip address in a
browser, e.g. `192.168.175.1`. Enter the password which has been defined during
router installation/setup. In a "local network" section of the configuration menu
select the BB and select "use static ip". Repeat the same for the host pc.

## SSH

check if ssh is already installed (if so something like `/usr/bin/ssh` should be displayed):

    which ssh

otherwise install ssh:

    sudo apt-get install ssh

connect from the host to the BB via ssh (confirm `Are	you	sure you want to
continue connecting (yes/no)?` with `yes` and enter the password, e.g. `temppwd`):

    ssh	debian@192.168.178.5

...you should see the command line of the BB:

    debian@beaglebone:~$

to exit the remote connection:

    debian@beaglebone:~$ exit

(BeagleBone Black Cookbook, p. 167)

## Transferring files between the host and BB

check if ssh is already installed (if so something like `/usr/bin/scp` should be displayed):

    which scp

otherwise install scp:

    sudo apt-get install scp

on the host to transfer a single file from the host to the BB (or `beaglebone` instead of `192.168.7.5`):

    touch test_host.txt
    scp test_host.txt debian@192.168.7.5:~

check if the file arrived at the BB (should print `test_host.txt`):

    ls | grep test_host.txt
