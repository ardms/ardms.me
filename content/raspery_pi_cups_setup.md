---
title: "Raspbery Pi Sway headless browser"
date: 2024-02-11
lastmod: 2024-02-11
draft: True
tags: ['personal progects']
---

# Introduction

Set up [CUPS](https://www.cups.org/) in order to print from any device at the
printer connected at the raspberry pi.

# Installing CUPS

```
sudo apt install cups
```

# Configure cupsd.conf
First backup the /ect/cups/cupsd.conf and then change the following

```
LogLevel warn
PageLogFormat
MaxLogSize 0
ErrorPolicy retry-job
Port 631
Browsing Yes
BrowseAddress All
DefaultAuthType Basic
WebInterface Yes
IdleExitTimeout 60
<Location />
  Order allow,deny
  Allow All
</Location>
<Location /admin>
  Order allow,deny
  Allow @LOCAL
</Location>
```
