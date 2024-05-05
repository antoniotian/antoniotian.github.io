---
layout: post
title: Playing Around with Raspberry Pi
subtitle: Raspberry Pi Basic User's Manual
author: Antoniotian (翰宝)
header-img: img/post-bg-raspberrypi-setup.jpg
header-mask: 0.4
tags:
  - Embedded System
  - Raspberry Pi
  - Raspberry Pi Guidebook
---

> Developed by the UK-based Raspberry Pi Foundation, the Raspberry Pi is a high-performance single-board computer. Its small size and low cost have quickly made it a very popular embedded device among DIYers, makers, electronics enthusiasts, and professional developers.

# Hardware Information of Raspberry Pi
---
The Raspberry Pi is a very popular device for developers and electronics enthusiasts due to its scalability, functionality and cost-effectiveness, not only for beginners and students but also for professionals.
### Raspberry Pi Model Comparison

|                   | Raspberry Pi 4B                                | Raspberry Pi 3B+                             | Raspberry Pi 3B                              | Raspberry Pi 2B                               |
| ----------------- | ---------------------------------------------- | -------------------------------------------- | -------------------------------------------- | --------------------------------------------- |
| Release Time      | 2019/06/24                                     | 2018/03/04                                   | 2018/03/04                                   | 2018/03/04                                    |
| SoC               | BCM2711                                        | BCM2837B0                                    | BCM2837                                      | BCM2836                                       |
| CPU               | ARM Cortex-A72 1.5GHz 64bit Quad-Core          | ARM Cortex-A53 1.4GHz 64bit Quad-Core        | ARM Cortex-A53 1.2GHz 64bit Quad-Core        | ARM Cortex-A7 900MHz 64bit Quad-Core          |
| Power Consumption | 600mA ~ 3000mA                                 | 500mA ~ 2500mA                               | 400mA ~ 2500mA                               | 350mA ~ 1800mA                                |
| Wi-Fi             | 2.4GHz/5GHz                                    | 2.4GHz/5GHz                                  | 2.4GHz                                       | N/A                                           |
| Bluetooth         | 5.0 BLE                                        | 4.2 BLE                                      | Bluetooth                                    | Bluetooth                                     |
| RAM               | 1/2/4/8 GB                                     | 1 GB                                         | 1 GB                                         | 1 GB                                          |
| USB               | USB 3.0x2、USB 2.0x2                            | USB 2.0x4                                    | USB 2.0x4                                    | USB 2.0X4                                     |
| Video Interface   | micro HDMI Port x2; Maximum resolution 4K 60Hz | HDMI (1.3,1.4); Maximum resolution 1920x1200 | HDMI (1.3,1.4); Maximum resolution 1920x1200 | HDMI (1.3,1.4) ; Maximum resolution 1920x1200 |
| Audio Interface   | 3.5mm micro HDMI                               | 3.5mm HDMI(1.3,1.4)                          | 3.5mm HDMI(1.3,1.4)                          | 3.5mm HDMI(1.3,1.4)                           |
| Power             | USB Type-C 5V                                  | MicroUSB 5V                                  | MicroUSB 5V                                  | MicroUSB 5V                                   |
| GPIO              | 40PIN                                          | 40PIN                                        | 40PIN                                        | 40PIN                                         |
| Dimension         | 85x56x17 mm                                    | 85x56x17 mm                                  | 85x56x17 mm                                  | 85x56x17 mm                                   |

### Raspberry Pi 4B PIN Definition
![Raspberry Pi PIN](/img/in-post-imag/post-inner-raspberry-pi-pin.png)
> The Raspberry Pi PIN definitions are available on the official website: [Raspberry Pi PIN Definitions](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)<br>
> Additional Tools Website：[Raspberry Pi Pinout](https://pinout.xyz) 

# Raspberry Pi OS Image Burn
---
### Preparation Work

| Hardware           | Software                                                                                    |
| ------------------ | ------------------------------------------------------------------------------------------- |
| SD Card, SD Reader | Raspberry Pi System Image Tool：[Raspberry Pi Imager](https://www.raspberrypi.com/software/) |

### Image Burn
Connect the SD card to the computer with a card reader, open the Raspberry Pi Image Tool. Select the appropriate Raspberry Pi model and system, as well as the SD memory card. Recommend the most recently released Raspberry Pi OS. Usually there will be a recommended system, Debian hardware support is better, so here we take Debian system as an example.
![系统写入_01](/img/in-post-imag/post-inner-raspberry-pi-imager-01.png)
You can choose to configure the Raspberry Pi OS system in advance before performing the burn-in. It is also possible to enter the system and set it up again after the burn is complete.
![系统写入_02](/img/in-post-imag/post-inner-raspberry-pi-imager-02.png)
Here is an example of advance system setup，click **「EDIT SETTINGS」**
![系统写入_03](/img/in-post-imag/post-inner-raspberry-pi-imager-03.png)
- **Set hostname：**hostname
- **Set username and password**
- **Set Wi-Fi：**The Wi-Fi list will not be displayed here, you need to fill in the SSDN of the Wi-Fi directly (i.e. the name that is displayed in the Wi-Fi list)
- **Language and time zone settings**

After completing the above settings, click **"SERVICES "**, check **"Enable SSH service "**, and choose to log in with a password. The password here is the user name and password set earlier.
![系统写入_04](/img/in-post-imag/post-inner-raspberry-pi-imager-04.png)
Click **"Save "** to start writing to the system.
![系统写入_05](/img/in-post-imag/post-inner-raspberry-pi-imager-05.png)
After burning, insert the SD card into the Raspberry Pi directly. After power on, the system will be initialised automatically.<br>
If the system is configured ahead of time, it will go straight to the desktop.<br>
If you don't set it up ahead of time, you can access the desktop with a simple system boot configuration.<br>
There are external display devices that can connect the Raspberry Pi to an external display device via HDMI.
> **Note:** The SD card will be formatted each time the system is burned, so you need to back up the data on the SD card before burning.

### Updata System
Once the system has finished loading, enter the desktop.The Raspberry Pi desktop is shown below:
![系统桌面](/img/in-post-imag/post-inner-raspberry-pi-desktop.png)
The first thing to do when the system installation is complete is to **Upgrade the system**, open the terminal and type in
```bash
sudo apt-get update
sudo apt-get upgrade
```
> **Note:** If the (Y/N) selection pops up during the upgrade process, enter Y and press Enter. The first upgrade may take a significant amount of time, so please be patient.

# 远程连接 Raspberry Pi
---
用 HDMI 连接屏幕太麻烦了，可以通过远程桌面连接树莓派。
### SSH 连接
SSH 是一种加密的远程连接网络协议，其主要用于远程管理系统和服务器。SSH 连接通过公钥加密来确保两台设备之间传输的数据是安全且保密的。建立连接后，SSH 通过命令行执行指令，如果连接对象是 Linux 系统，则直接用终端指令即可对远程设备进行控制。

在 Raspberry Pi 中开启 SSH 服务的方法有两种：
- 从图形界面进行设置
- 通过命令行进行设置

#### 从图形界面进行设置
点击**「Menu」➡️「Preference」➡️「Raspberry Pi Configuration」**如下图所示
![系统配置](/img/in-post-imag/post-inner-raspberry-pi-config01.png)
打开 SSH 开关，同时建议全部打开
![系统配置](/img/in-post-imag/post-inner-raspberry-pi-config02.png)

#### 通过命令行进行设置
在终端中输入
```bash
sudo raspi-config
```
选择 `Interface Options` -> `SSH` 开启 SSH，如下图所示：
![系统配置](/img/in-post-imag/post-inner-raspberry-pi-config03.png)
#### 通过其他主机连接 SSH
以 macOS 系统为例，Windows 的指令是一样的。
在 macOS 终端中输入：
```bash
ssh username@ip_address
```
![SSH 连接](/img/in-post-imag/post-inner-raspberry-pi-ssh-01.png)
连接时，提示是否建立连接，输入 `yes` 然后回车，再输入密码就能够建立 SSH 连接了。密码和 Raspberry Pi 的登陆密码一致。
![SSH 连接](/img/in-post-imag/post-inner-raspberry-pi-ssh-02.png)
如果连接过程中出现以下画面：
![SSH 连接错误](/img/in-post-imag/post-inner-raspberry-pi-ssh-error.png)
则需要输入
```bash
ssh-keygen -R <Host_IP>
```
这是由于目标设备接收到 SSH 连接请求的密钥和存储在设备上的密钥不匹配。出于安全考虑，SSH客户端默认不会连接到具有不匹配密钥的主机。而上述的指令相当于是为了连接 SSH，让主机重新创建一个密钥。

## VNC 连接
VNC 连接提供一种可视化的远程桌面连接服务，让开发者能够直接以图形界面操作树莓派。用 VNC 连接树莓派需要下载 VNC软件：
[RealVNC](https://www.realvnc.com/en/connect/download/combined/)

> 在设置 SSH 连接的时候，我们已经开启了 VNC 服务。如果连接不成功，请检查 VNC 服务是否开启。

![VNC 连接](/img/in-post-imag/post-inner-raspberry-pi-vnc-01.png)
直接输入 Raspberry Pi 的 IP 地址，填入用户名和密码就能通过 VNC 连接树莓派的远程桌面了。
![VNC 连接](/img/in-post-imag/post-inner-raspberry-pi-vnc-02.png)

_感谢使用该教程，作者将持续更新教程和 Raspberry Pi 相关信息。😊_