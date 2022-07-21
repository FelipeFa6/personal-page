---
title: "Arch BIOS Install"
date: 2022-07-20T23:50:34-04:00
tags: ['arch','guide']
draft: false
---

[Go Back...](/guides)

Should be connected to the internet via cable, for wifi refer to the arch wiki.

# Sync time protocol

```sh
$ timedatectl set-ntp true
```

# Partitions Get disks

```sh
$ lsblk
```

# Enter your hardware storage

```sh
$ fdisk /dev/sdx
```

# Partition the disks as you like.
For this tutorial i will be doing 2 partitions

> SWAP partition with 10GB
> Storage partition with remaining space. (Remember to put the BOOT flag with 'a' in fdisk)

# Format the partitions
This is the storage partition
```sh
$ mkfs.ext4 /dev/sdx
```

# Format SWAP partition.
```sh
$ mkswap /dev/sdxN
```

# Mount of partitions
Storage partition
```sh
$ mount /dev/sdxN /mnt
```

Mount SWAP partition
```sh
$ swapon /dev/sdx
```

# Installing base system
```sh
$ pacstrap /mnt base base-devel linux-lts linux-firmware vim git networkmanager
```
# Generate FSTAB
```sh
$ genfstab -U /mnt >> /mnt/etc/fstab
```

# Change installation medium
```sh
$ arch-chroot /mnt
```

# Enable NetworkManager
```sh
$ systemctl enable NetworkManager
```

# Timezone
```sh
$ ln -sf /usr/share/zoneinfo/Chile/Continental /etc/localtime
$ hwclock --systohc
```

# Change locale.gen
Edit the /etc/locale.gen file and uncomment your language, in my case is
en_US-UTF-8 UTF-8
Enter the following command:
```sh
$ locale-gen
```

# Edit locale.conf
```sh
$ echo "LANG=en_US.UTF-8" >> /etc/locale.conf
```

# Add hostname

$ echo "yourHostName" > /etc/hostname

# Add hosts
Edit /etc/hosts:
```sh
127.0.0.1   localhost
::1   localhost
```

# Add a password to your root
```sh
$ passwd
```

# Set the bootloader
Download following software
```sh
$ pacman -S grub
```

# GRUB install
Do this to the whole device where Arch is installed

```sh
$ grub-install /dev/sdx
$ grub-mkconfig -o /boot/grub/grub.cfg
$ mkinitcpio -P
```

# Add new user
```sh
$ useradd -mG wheel newUser
$ passwd newUser
```

RESTART YOUR SYSTEM AND YOU ARE READY TO GO.
