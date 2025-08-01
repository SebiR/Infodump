# Using the Huawei E3372 4G Surfstick on OpenWrt

## Prerequisites

- Huawei E3372h or E3372s in HiLink mode (stick acts as a router, usually with IP 192.168.8.1)
- Open WRT router with USB host port
- Access to the OpenWrt terminal via SSH (altough LuCI would suffice)

## Step 1: Connect the Surf Stick

Plug the Huawei E3372 into the USB port of your OpenWrt router (but you've probably already done this).
And your computer has be connected to the router via ethernet or wifi.

## Step 2: Install Required Packages

Use an SSH client to connect to your router:

```bash
ssh root@192.168.1.1
```
Replace `192.168.1.1` with the IP address of your OpenWrt router if different.


Run the following commands via SSH:

```sh
opkg update
opkg install kmod-usb-net-cdc-ether
opkg install usb-modeswitch
```


## Step 3: Configure Network Interface

> When you use LuCI, go to **Network > Interfaces > Add New Interface** and add the two interfaces mentioned down below.

Edit the network configuration:

```bash
vi /etc/config/network
```

Add a new interface for IPv4:
```sh
config interface 'wan4'
    option ifname 'eth1'         # Replace with correct interface name
    option proto 'dhcp'

config interface 'wan6'
    option ifname 'eth1'         # Same interface
    option proto 'dhcpv6'

```

Save and quit vi and apply the configuration:

```bash
/etc/init.d/network reload
```

To verify:

```bash
ifstatus wan4
ifstatus wan6
```
