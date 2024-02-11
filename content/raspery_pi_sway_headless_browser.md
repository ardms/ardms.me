---
title: "Raspbery Pi Sway headless browser"
date: 2024-02-11
lastmod: 2024-02-11
draft: True
tags: ['personal progects']
---

# Introduction

I wanted to have a rapberry Pi constantly connected to my TV with a VPN connection to a different part of the world so I can watch un-cencored content whenever I want from my TV.

## Summary
Idea is to have [sway](www.swaywm.org) installed on Raspberry Pi OS Lite that will be configures so on boot establises a VPN connection and then loads a browser.  
  
## Install and configure Sway

To install sway just run:

`sudo apt install sway`

An easy way to start sway on login. Add the following to your _bash_profile_

`[ "$(tty)" = "/dev/tty1" ] && exec sway`

