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

### 树莓派4B PIN 脚定义
![Raspberry Pi PIN](/img/in-post-imag/post-inner-raspberry-pi-pin.png)
> Raspberry Pi 的 PIN 定义在官方网站中可以查阅:[Raspberry Pi 官方网站](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)<br>
> 另外工具网站：[Raspberry Pi Pinout](https://pinout.xyz) 中对 PIN 脚有详细的说明

# Raspberry Pi OS 系统写入
---
### 准备工作


| 硬件        | 软件                                                                     |
|-----------|------------------------------------------------------------------------|
| SD 卡      | 树莓派系统写入工具：[Raspberry Pi Imager](https://www.raspberrypi.com/software/) |
| SD 读卡器    |                                                                        |   


### 系统写入
将 SD 卡用读卡器连接电脑，打开树莓派写入工具，选择合适的 Raspberry Pi 型号和系统，以及 SD 存储卡。系统优先选择最近发布的 Raspberry Pi OS，一般会有推荐系统。Debian 的硬件支持更好，所以这里以 Debian 系统为例。
![系统写入_01](/img/in-post-imag/post-inner-raspberry-pi-imager-01.png)
在执行烧录之前，可以选择提前对 Raspberry Pi OS 系统进行配置。
也可以烧录完成后，进入系统再设置。
![系统写入_02](/img/in-post-imag/post-inner-raspberry-pi-imager-02.png)
这里以提前进行系统设置为例，点击**「编辑设置」**
![系统写入_03](/img/in-post-imag/post-inner-raspberry-pi-imager-03.png)
- **设置主机名称：**主机名称
- **设置用户名和密码**
- **配置 Wi-Fi：**这里不会显示 Wi-Fi 列表，需要直接填写 Wi-Fi 的 SSDN（即显示在Wi-Fi列表中的名字）
- **语言和时区设置**

完成上述设置之后，点击**「SERVICES」**，勾选**「开启SSH服务」**，并选择使用密码登陆。这里的密码就是前面设置的用户名和密码。
![系统写入_04](/img/in-post-imag/post-inner-raspberry-pi-imager-04.png)
点击**「保存」**，开始写入系统。
![系统写入_05](/img/in-post-imag/post-inner-raspberry-pi-imager-05.png)
烧录完成后，直接将 SD 卡插入 Raspberry Pi 即可。通电后，系统会自动初始化。<br>
如果提前配置了系统，就会直接进入桌面。<br>
如果没有提前设置，只需通过简单的系统引导配置，就可以进入桌面了。<br>
有外界显示设备可以通过 HDMI 连接 Raspberry Pi 与外部显示设备。
> **注意：** 每次系统烧录都会格式化 SD 卡，因此在烧录之前需要备份好 SD 卡中的数据

### 升级系统
系统加载完成后，进入桌面。Raspberry Pi 桌面如下所示：
![系统桌面](/img/in-post-imag/post-inner-raspberry-pi-desktop.png)
系统安装完成的第一件事就是**升级系统**，打开终端，输入
```bash
sudo apt-get update
sudo apt-get upgrade
```
> **注意：** 如果在升级的过程中弹出 (Y/N) 选择，输入 Y 后按回车即可。首次升级可能需要花费大量的时间，请耐心等待。

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