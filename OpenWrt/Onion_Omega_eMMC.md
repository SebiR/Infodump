> [!CAUTION]
> This tutorial is currently AI generated and will be tested by a real human. If this note disappears, the tutorial worked

# Expanding OpenWrt Root Filesystem to eMMC Storage

## Prerequisites
- An OpenWrt device with an attached eMMC storage.
- Basic knowledge of Linux command-line operations.
- Access to the OpenWrt terminal via SSH.
- Installed tools:
```sh
opkg install lsblk fdisk
```

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

## Step 2: Partition the eMMC Storage
If the eMMC storage is not already partitioned, use `fdisk`:

```sh
fdisk /dev/mmcblk0
```

Follow these steps inside `fdisk`:
1. Press `n` to create a new partition.
2. Select `p` for primary partition.
3. Choose a partition number (usually `1`).
4. Accept default values for start and end sectors.
5. Press `w` to write changes and exit.

Format the partition as ext4:

```sh
mkfs.ext4 /dev/mmcblk0p1
```

## Step 3: Mount eMMC Storage
Create a mount point and mount the newly created partition:

```sh
mkdir /mnt/emmc
mount /dev/mmcblk0p1 /mnt/emmc
```

## Step 4: Copy Root Filesystem to eMMC
Use `tar` to copy the current root filesystem to the eMMC:

```sh
tar -cvpzf /mnt/emmc/rootfs.tar.gz --exclude=/mnt --exclude=/proc --exclude=/sys --exclude=/dev --exclude=/run --exclude=/tmp /
cd /mnt/emmc
mkdir rootfs
cd rootfs
sudo tar -xvzf ../rootfs.tar.gz
```

## Step 5: Configure OpenWrt to Boot from eMMC
Modify the boot configuration to mount the new root filesystem.

Edit `/etc/fstab`:

```sh
echo '/dev/mmcblk0p1 / ext4 defaults 0 1' >> /etc/fstab
```

Ensure the kernel loads the new root filesystem by modifying the bootloader settings.
For devices using `GRUB`, update `grub.cfg` to point to `/dev/mmcblk0p1`.
For devices using `U-Boot`, update `bootargs` accordingly:

```sh
setenv bootargs root=/dev/mmcblk0p1 rootfstype=ext4 rw
saveenv
```

## Step 6: Reboot and Verify
Reboot the device:

```sh
reboot
```

After reboot, verify that the root filesystem is now on the eMMC storage:

```sh
df -h /
```

It should now show `/dev/mmcblk0p1` as the root filesystem.

## Conclusion
You have successfully expanded the OpenWrt root filesystem onto eMMC storage, increasing storage capacity and improving performance.

