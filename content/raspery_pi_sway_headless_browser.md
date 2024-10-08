---
title: "Raspbery Pi Sway headless browser"
date: 2024-02-11
modified: 2024-09-29
draft: True
tags: ['personal progects']
---

# Introduction

I wanted to have a rapberry Pi constantly connected to my TV with a VPN
connection to a different part of the world so I can watch un-cencored content
whenever I want from my TV.

## Summary
Idea is to have [sway](www.swaywm.org) installed on Raspberry Pi OS Lite that
will be configures so on boot establises a VPN connection and then loads a
browser.  
  
## Activate Wayland

You will need too run raspi-config and then navigate to `Advance option > Wayland`

## Install and configure Sway

To install sway just run:

`sudo apt install sway`

An easy way to start sway on login. Add the following to your _bash_profile_

`[ "$(tty)" = "/dev/tty1" ] && exec sway`

## Set up autologin

Run: sudo raspi-config
Choose option: 1 System Options
Choose option: S5 Boot / Auto Login
Choose option: B2 Console Autologin
Select Finish, and reboot the Raspberry Pi.

## Change resolution/scale if using a big screen
I found this the best way to increase font size and make everything more visible. 
Follow instructions at [Arch wiki](https://man.archlinux.org/man/sway-output.5.en)

First you need to find the display you are using. You will need to do the following but not through __ssh__ as it will not show you any display.

`swaymsg -t get_outputs`

Once you have the output then  you will need to add the following to your .config:

`output HDMI-A-1 scale 3`

pactl set-sink-volume @DEFAULT_SINK@ +5%

I finally decided to change scree resolution and not scale. I was having the problem explained [here](https://blogs.kde.org/2024/10/09/cursor-size-problems-in-wayland-explained/) Scaling had some anoying artifacts including mouse cursor not displaying properly

## VPN connection

### NordVPN
For now I'm using NordVPN. One easy way to set this up in Linux is to use a Token
For instalation nordvpn executable see [link](https://support.nordvpn.com/hc/en-us/articles/20196094470929-Installing-NordVPN-on-Linux-distributions?_gl=1*3tyuwm*_gcl_au*MTYzNjU0NTQ0MC4xNzI2OTQ5NTAz*FPAU*MTYzNjU0NTQ0MC4xNzI2OTQ5NTAz*_ga*MzMwMTkzODkyLjE2OTY3ODAxMTc.*_ga_LEXMJ1N516*MTcyNjk0OTUwMy42LjEuMTcyNjk0OTY4OS41NS4wLjA.)
To create and use the token see [link](https://support.nordvpn.com/hc/en-us/articles/20286980309265-How-to-use-a-token-with-NordVPN-on-Linux)

Once the token is generated then just use
```
nordvpn login --token <token>
```

To autologin on startup
```
nordvpn set autologin Greece Athens
```

A small problem that VPN creates is that I was not able to __ssh__ into the
raspberrypi from my local network any more. To solve this issue I have used
the
[meshnet](https://meshnet.nordvpn.com/getting-started/how-to-start-using-meshnet/using-meshnet-on-linux)
by setting
```
nordvpn set meshnet on
```
Meshnet will be set on and remain on even after a reboot.

### Disable ssh login as root
Because of the above it will be wise to disable login as root. To do that

## Start Firefox on startup

Edit `.config/sway/config` and add the following
```
execute Firefox
```

Hope Raspberrypi I'm using now (5 2GB) is able to stream....

## Set up wlogout
Found this handy wayland logout menu [wlogout](https://github.com/ArtsyMacaw/wlogout)
Setup is really easy. Just copy everything from `/etc/wlogout/` into `~/.config/wlogout/`
Then add into `~/.config/sway/config` the following
```
bindsym $mod+Shift+e exec wlogout
```

