---
title: "How to google drive on Linux"
date: 2024-06-27
lastmod: 2024-06-27
draft: false
---

# Intro

A solution to sync my Google Drive files into my Linux Debian laptop. One of the main obgectives is to have a solution that is as open-source as possible and at the same time as configurable as possible.

# RCLONE
I had a look at [this](https://rclone.org/). 

## installation
This was the easy part just visit the [Download](https://rclone.org/downloads/) page and download the deb file

## configutaion
First run `rclone config`. You will need to log in to your goodle account from a browser.

## Mount all folders manualy
You will need fuse3 installed in your system. This can be done with `sudo apt install fuse3`

Then you can mount the drive by doing the following
```
rclone mount remote: ~/mnt --cache-db-purge --fast-list --poll-interval 10m
```

Where _remote_ is the name you have chosen during the configuration

## Configuring Systemd

Manually running the rclone mount command will work but does not persist between reboots or run automatically

To make this process happen, navigate to /etc/systemd/system.  Here, you will want to make a new .service file that will let us automatically have rclone mount when the machine boots up.

Create a file named gdrive.service and edit it with a text editor of your choosing.

```
[Unit]
Description=rclone for gdrive_mount
AssertPathIsDirectory=/mnt/gdrive
After=networking.service

[Service]
Type=simple
ExecStart=rclone mount --config=/home/tcude/.config/rclone/rclone.conf remote: /mnt/gdrive --cache-db-purge --poll-interval 10m
ExecStop=/bin/fusermount -u /mnt/gdrive
Restart=always
RestartSec=10

[Install]
WantedBy=default.target
```
