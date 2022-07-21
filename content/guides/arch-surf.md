---
title: "Arch SURF Browser"
date: 2022-07-20T23:51:06-04:00
tags: ['arch','guide']
draft: false
---

[Go Back...](/guides)

# Clone Surf
```sh
$ git clone https://git.suckless.org/surf
```

# Install the following dependencies.
```sh
$ pacman -S webkit2gtk gcr
```

# Compile Surf
```sh
$ sudo make clean install
```

# Extra packages for surf
By default surf cant play youtube videos.
Your system will need the following packaged for it to work.
```sh
$ pacman -S gstreamer gst-plugins-good gst-libav gst-plugins-base xdg-utils
```
