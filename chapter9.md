# Remote control

## SSH

A typical private network looks like this:

![Interface the BB via Ethernet](diagrams/BB_remote_access.png)

get the ip address of the BB and host with `eth0` as interface, on each:

    ifconfig eth0 | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}'

get the ip address of the router:

    netstat -nr | awk '$1 == "0.0.0.0"{print$2}'

connect from the host to the BB via ssh (confirm `Are	you	sure you want to
continue connecting (yes/no)?` with `yes` aand enter the password, e.g. `temppwd`):

    ssh	debian@192.168.178.5

you should see the command line of the BB:

    debian@beaglebone:~$

(BeagleBone Black Cookbook, p. 167)
