---
title: "home-assistance-raspberryPi"
date: 2023-09-16
lastmod: 2023-09-17
draft: false 
tags: ['personal progects']
---

# Home assistance installation

## Summary

I thought this would be easier. I have an old raspberryPi 3 that I use for several tasks like having a network printer with [CUPS](https://www.cups.org/) having a small display to show weather and bus times. Because of that I didn't want to flash the [Home Assisntant Operating System](https://www.home-assistant.io/installation/raspberrypi) but rather an instance of Home Assistant that would run in a container inside the [Raspberry Pi OS Lite ](https://www.raspberrypi.com/software/operating-systems/). 

I first followed the instructions and installed Home Assistant Container only to find out that this is not what I wanted since it is not allowing you to install add-ons so after looking into the [guide](https://www.home-assistant.io/installation/) I understood that what I needed was [Home Assistant Supervised](https://community.home-assistant.io/t/installing-home-assistant-supervised-on-a-raspberry-pi-using-debian-12/247116)

## Docker installation

`curl -sSL https://get.docker.com | sh`

`sudo usermod -aG docker $USER`

## Install OS Agent and Dependencies

First install dependencies

`sudo apt install apparmor jq wget curl udisks2 libglib2.0-bin network-manager
dbus lsb-release systemd-journal-remote systemd-resolved -y`

Then install os-agent _note the version_

```
wget https://github.com/home-assistant/os-agent/releases/download/1.6.0/os-agent_1.6.0_linux_aarch64.deb

sudo dpkg -i os-agent_1.6.0_linux_aarch64.deb
```

## Install Home Assistant Supervised

```
wget https://github.com/home-assistant/supervised-installer/releases/latest/download/homeassistant-supervised.deb

sudo dpkg -i homeassistant-supervised.deb 
```

If there are any issues with installation you can try 

`ha jobs options --ignore-conditions healthy`

Once the above is completed you should be able to connect to home assistance instance at:

`http://<host>:8123`

# Home assistance setup

## Set up electricity smart meter readings

- Setting up an account – First you’ll need to setup an account with the only
DCC authorised agent, “Glow”. There is no easy way to do this on desktop –
so you’ll need to download the “Bright” app for either iOS or Android. Once
you’ve downloaded the app, go through the sign up process (you’ll need your
details) and provide your meter details from your IHD. You should start
seeing readings appear instantly in the app. 
- Setup the Home Assistant
Integration – The plugin I recommend is HandyHat’s integration available on
[GitHub](https://github.com/HandyHat/ha-hildebrandglow-dcc). You can follow his instructions for automated installation via
HACS, but I prefer the manual method, so download the files and drop them
in your config directory (I recommend using the Samba plugin to achieve
this).
- Setup the integration – Here’s the easy bit – create a new integration and
select the “Hildebrand Glow (DCC)” integration, enter your glow details from
step 1 – and your energy usage should now be available in Home Assistant!

## Set up Local Bytes Smart Plug

- First you need to install [MQTT broker](https://github.com/home-assistant/addons/blob/master/mosquitto/DOCS.md). Follow instruction on github account
- Then you need to install [MQTT](https://www.home-assistant.io/integrations/mqtt/).
- Last you need to install [TASMOTA](https://www.home-assistant.io/integrations/tasmota/)

### Configure Smart Plug by:

- Power on the device. This may be plugging it in to the wall, or turning on a light switch.
- Open the Wi-Fi settings on your Mobile Device/Computer.
- Wait until you see a Wi-Fi network that starts with tasmota, join it. Eg "tasmota-ebaec4"
- Either open a browser to 192.168.4.1, or click on the "Sign in to this network" prompt.
- You'll be presented with a list of Wi-Fi networks, select yours and type in the password.
- Take note of the IP address that you are presented with.
- Your browser should automatically redirect to the devices new IP address.
- Click "Configure Other" and update the Device Name & Friendly Name 1, then click save.
- We recommend using the same name value for both
- Click "Configure MQTT" and fill in the following details:
- Host - The IP address of you MQTT instance. (Starting on Tasmota 12.1.1, you can use homeassistant.local).
- Client - This must be unique for the user. The default value will work.
- User - Use the user you previously created.
- Password - Use the password you previously created.
- Click Save

