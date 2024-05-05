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
sudo apt-get install bluetooth bluez rfcomm
```

### Configure the Bluetooth Service
Use the `bluetoothctl` utility to configure Bluetooth so that the Raspberry Pi is visible to and can pair with other Bluetooth devices. After entering the `bluetoothctl` command line interface, you can use the following commands:
```
sudo bluetoothctl 
power on 
agent on 
default-agent 
discoverable on 
pairable on
```
`power on`: Bluetooth hardware will be powered on when the system started up. 

`agent on`: This command enables the agent that handles pairing requests. The agent is responsible for automatically responding to requests that would otherwise require user interaction, such as entering a PIN. Turning the agent on streamlines the pairing process by managing these interactions programmatically.

`default-agent`: Sets the currently active agent as the default agent. This means that this agent will handle all future pairing and trust requests.

`discoverable on`: 

`pairable on`: 