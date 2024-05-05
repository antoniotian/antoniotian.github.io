---
layout: post
title: Connect Raspberry Pi with Bluetooth
subtitle: Use Bluetooth to get access terminal of Raspberry Pi
author: Antoniotian (翰宝)
header-img: img/post-bg-raspberrypiconnectwithbt.jpeg
header-mask: 0.4
tags:
  - Embedded
  - System
  - Raspberry
  - Pi
  - Raspberry
  - Pi
  - Guidebook
---

> Using Bluetooth to control terminals can offer unique advantages in certain situations, though it is not always the preferred method of communication in all environments. In the absence of available WI-FI networks or when wired connections are inconvenient, Bluetooth provides a handy wireless connection option. 

# Bluetooth Access Setup
---
To access the Raspberry Pi terminal over Bluetooth, you'll need to set up the Raspberry Pi so that it can accept connections via Bluetooth and provide terminal access. This involves several steps including installing necessary software, configuring the Bluetooth device, and setting up a secure connection. 
### Update the System and Install Bluetooth Utilities
Update your Raspberry Pi system with terminal
```
sudo apt update
sudo apt upgrade
```
Install Bluetooth-related packages
```
sudo apt install bluetooth bluez blueman
```