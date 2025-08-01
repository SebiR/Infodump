# Using the Huawei E3372 4G Surfstick on OpenWrt

## Prerequisites
- Huawei E3372h or E3372s in HiLink mode (stick acts as a router, usually with IP 192.168.8.1)
- Open WRT router with USB host port
- Access to the OpenWrt terminal via SSH (altough LuCI would suffice)

## Step 1: Identify eMMC Storage
First, determine the device name assigned to the eMMC storage.

```sh
lsblk
```

or

```sh
fdisk -l
```

The eMMC storage is usually named `/dev/mmcblk0` or similar.

## Step 2: Install Required Packages
Run the following commands via SSH:

```sh
opkg update
opkg install kmod-usb-net-cdc-ether
opkg install usb-modeswitch
```

## Step 3: Configure Network Interface
Create a mount point and mount the newly created partition:

```sh
config interface 'wan4'
    option ifname 'eth1'         # Replace with correct interface name
    option proto 'dhcp'

config interface 'wan6'
    option ifname 'eth1'         # Same interface
    option proto 'dhcpv6'

```

