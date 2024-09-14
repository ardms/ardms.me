---
title: "Raspbery Pi Sway headless browser"
date: 2024-02-11
lastmod: 2024-02-11
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

## Change scale if using a big screen
I found this the best way to increase font size and make everything more visible. 
Follow instructions at [Arch wiki](https://man.archlinux.org/man/sway-output.5.en)

First you need to find the display you are using. You will need to do the following but not through __ssh__ as it will not show you any display.

`swaymsg -t get_outputs`

Once you have the output then  you will need to add the folloing to your .config:

`output HDMI-A-1 scale 3`

pactl set-sink-volume @DEFAULT_SINK@ +5%



