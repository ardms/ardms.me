---
title: "Raspbery Pi CUPS setup"
date: 2024-02-11
modified: 2024-09-29
draft: False
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
First backup /ect/cups/cupsd.conf and then change the following

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
