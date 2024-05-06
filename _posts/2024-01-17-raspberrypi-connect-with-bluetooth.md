---
layout: post
title: Connect Raspberry Pi with Bluetooth
subtitle: Use Bluetooth to get access terminal of Raspberry Pi
author: Antoniotian (翰宝)
header-img: img/post-bg-raspberrypiconnectwithbt.jpeg
header-mask: 0.4
tags:
  - Embedded System
  - Raspberry Pi
  - Raspberry Pi Guidebook
---

> Using Bluetooth to control terminals can offer unique advantages in certain situations, though it is not always the preferred method of communication in all environments. In the absence of available WI-FI networks or when wired connections are inconvenient, Bluetooth provides a handy wireless connection option. 

# Bluetooth Access Setup
---
To access the Raspberry Pi terminal over Bluetooth, you'll need to set up the Raspberry Pi so that it can accept connections via Bluetooth and provide terminal access. This involves several steps including installing necessary software, configuring the Bluetooth device, and setting up a secure connection. 
### Update the System and Install Bluetooth Utilities
Update your Raspberry Pi system with terminal
```bash
sudo apt update
sudo apt upgrade
```
Install Bluetooth-related packages
```bash
sudo apt-get install bluetooth bluez blueman rfcomm
```

### Configure the Bluetooth Service
Use the `bluetoothctl` utility to configure Bluetooth so that the Raspberry Pi is visible to and can pair with other Bluetooth devices. After entering the `bluetoothctl` command line interface, you can use the following commands:
```bash
sudo bluetoothctl 
power on 
agent on 
default-agent 
discoverable on 
pairable on
exit
```
`power on`: Bluetooth hardware will be powered on when the system started up. <br>
`agent on`: This command enables the agent that handles pairing requests. The agent is responsible for automatically responding to requests that would otherwise require user interaction, such as entering a PIN. Turning the agent on streamlines the pairing process by managing these interactions programmatically.<br>
`default-agent`: Sets the currently active agent as the default agent. This means that this agent will handle all future pairing and trust requests.<br>
`discoverable on`: This command makes the Bluetooth device discoverable to other Bluetooth devices.<br>
`pairable on`: Enables the pairing mode on your Bluetooth device, allowing other devices to pair with it.<br>
`exit`: Exit the Bluetooth control interface.<br>
![Terminal Example Display](/img/in-post-imag/post-inner-raspberry-pi-bluetooth-01.png)

### Setup RFCOMM Service
If the file `/etc/systemd/system/rfcomm.service` exist in your system, you can just open it with `nano` or `vim`.<br> 
As `nano` an example: `sudo nano /etc/systemd/system/rfcomm.service`.<br>
OR, if there is no such file in your system, you still can use `sudo nano /etc/systemd/system/rfcomm.service` to create the file, and configure the RFCOMM service:<br>
![Terminal Example Display](/img/in-post-imag/post-inner-raspberry-pi-bluetooth-02.png)<br>
After you finished edit the file, press `Ctrl+O` and `Enter` to Write Out (Save).<br>
Press `Ctrl+X` to Exit.<br>

Reload the service configuration and start the service:
```bash
sudo systemctl daemon-reload
sudo systemctl start rfcomm.service
sudo systemctl enable rfcomm.service
```
After completing the above setup, you can connect to the Raspberry Pi from any device that supports the Bluetooth Serial Port Profile (SPP).Here I'm using a MacBook as an example, the steps for Windows are basically the same. It's just that Windows may require the use of a tool like PuTTY.<br>
Connect to the Raspberry Pi with Bluetooth.<br>
Usually, it requires the PIN code. The default PIN are `0000` or `1234`.<br>
![Terminal Example Display](/img/in-post-imag/post-inner-raspberry-pi-bluetooth-03.png)<br>
> **Note:** If neither of the above default PIN Codes allow for a connection, you will need to set up the connection for the first time on the Raspberry Pi. Don't worry, after configuring the first time connection, if you complete the above Bluetooth configuration, you will be able to automatically connect to the host computer the next time the Raspberry Pi is powered on and will no longer need a PIN code!

# Connect from Another Device
After completing the above setup, you can connect to the Raspberry Pi from any device that supports the Bluetooth Serial Port Profile (SPP).

### Mac OS
```bash
ls /dev/tty.*
screen /dev/tty.raspberrypi 115200
```
You can connect to the Raspberry Pi's terminal after input your `user name` and `password`.<br>
![Terminal Example Display](/img/in-post-imag/post-inner-raspberry-pi-bluetooth-04.png)

To disconnect, simply press `Ctrl-A` , then press `k`. Answer `y` to confirm. <br>
This will kill the current screen session. You will be asked if you really want to quit the screen session. 