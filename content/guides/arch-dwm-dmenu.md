---
title: "Arch Dwm Dmenu"
date: 2022-07-20T23:50:53-04:00
tags: ['arch','guide']
draft: false
---

[Go Back...](/guides)

# dwm & dmenu
Install the following dependencies
```sh
$ pacman -S xorg-server xorg-xini libxinerama libxft webkit2gtk
```

# Clone dwm & dmenu
```sh
$ git clone https://git.suckless.org/dwm
$ git clone https://git.suckless.org/dmenu
```

# Compile the cloned repos with
```sh
$ doas make clean install -C /path/to/dwm
$ doas make clean install -C /path/to/dmenu

```

# Create a X config file
```sh
$ echo "exec dwm" > ~/.xinitrc
```
