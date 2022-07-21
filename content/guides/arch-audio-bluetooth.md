---
title: "Arch Audio Bluetooth"
date: 2022-07-20T23:50:46-04:00
tags: ['arch','guide']
draft: false
---

[Go Back...](/guides)

# Audio

```sh
$ pacman -S pulseaudio pulsemixer
```


There some time that pulseaudio does not work out of the box. To fix this isue, we need to start it with the following command:

```sh
$ pulseaudio &
```

# Bluetooth

```sh
$ pacman -S bluez bluez-utils pulseaudio-bluetooth
```

Start/Enable Bluetooth Services:

```sh
$ doas systemctl start bluetooth
```

## Connecting and Pairing

Use the Bluetooth CLI:
```sh
$ bluetoothctl
```

Now run the following to setup bluetooth.

```sh
[bluetooth]# power on
[bluetooth]# agent on
[bluetooth]# default-agent

```
The next step is scanning near devices and pairing to them.

In my case I have a HUAWEI FreeBuds and we will use the _ MAC Adress _ to pair and connect to them.

```sh
[bluetooth]# scan on
[NEW] Device 2C:C5:46:5F:B8:29 HUAWEI FreeBuds Pro
[bluetooth]# pair 2C:C5:46:5F:B8:29
[bluetooth]# connect 2C:C5:46:5F:B8:29

```

Finally, if you want to automatically connect to this device in the future:
```sh
[bluetooth]# trust 2C:C5:46:5F:B8:29
```

## "Power on" on System startup
Bluetooth is not powered on startup or after resume.

To enable this go to /etc/bluetooth/main.conf , uncomment and set to true the following:

```sh
[Policy]
AutoEnable=true
```
