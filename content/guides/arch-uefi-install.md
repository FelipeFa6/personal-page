---
title: "Arch UEFI Install"
date: 2022-07-20T23:50:28-04:00
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
For this tutorial I will be doing 2 partitions.
- 200MB UEFI partition
- EFI System (press t and then 1 for EFI) Full storage
- Remaining size.

# Format partitions EFI Partition
```sh
$ mkfs.fat -F32 /dev/sdx
$ mkfs.ext4 /dev/sdx
```

# Mount of partitions
Storage partition
```sh
$ mount /dev/sdx /mnt
```

# EFI partition
```sh
$ mkdir /mnt/boot/
$ mount /dev/sdx /mnt/boot
```

# Installing base system
```sh
$ pacstrap /mnt base base-devel linux-lts linux-firmware vim git
```

For WiFi Internet add:
```sh
dhpcd iwd
```

For Wired Internet add:
```sh
networkmanager
```

# Generate FSTAB
```sh
$ genfstab -U /mnt >> /mnt/etc/fstab
```

# Change installation medium
```sh
$ arch-chroot /mnt
```

# Create SWAP file.
```sh
$ fallocate -l 2GB /swapfile
$ chmod 600 /swapfile
$ mkswap /swapfile
$ swapon /swapfile
```

# Add SWAPFILE to FSTAB
```sh
$ echo "/swapfile none swap defaults 0 0" >> /etc/fstab
```

# Timezone
```sh
$ ln -sf /usr/share/zoneinfo/Chile/Continental /etc/localtime
$ hwclock --systohc
```

# Change /etc/locale.gen
Use a text editor to edit this file and search for your use case.
This is used to use your local standards (More info [here](https://wiki.archlinux.org/title/Locale))

In my case, I'll use a shortcut.

```sh
$ echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
```
# Generate the locale
```sh
$ locale-gen
```

# Edit locale.conf
```sh
$ vim /etc/locale.conf
```

# Add hostname
```sh
$ echo "yourHostName" >> /etc/hostname
```


# Edit /etc/hosts
```sh
127.0.0.1   localhost
::1         localhost
```

# Secure your root user
```sh
$ passwd
```

# Set grub (boot loader)

```sh
#Download GRUB and EFIBOOTMGR
$ pacman -S grub efibootmgr
$ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
$ grub-mkconfig -o /boot/grub/grub.cfg
```

# Add New User
```sh
$ useradd -mG wheel newUser
$ passwd newUser
```

RESTART YOUR SYSTEM AND YOU ARE READY TO GO.


