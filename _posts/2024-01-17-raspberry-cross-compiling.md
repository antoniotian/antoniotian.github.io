---
layout: post
title: QT 与 Raspberry Pi 的交叉编译
subtitle: QT 基于 ARM 架构的交叉编译器
author: Antonio
header-img: img/post-bg-css.jpg
header-mask: 0.4
tags:
  - 嵌入式系统
  - Linux
  - QT
  - RaspberryPi
  - 树莓派
---

> 什么是交叉编译？
> 交叉编译是指在编译性能更加强大的宿主 (host) 计算机中生成能够提供给另一平台 (target) 可运行代码的过程。

# QT 交叉编译 Raspberry Pi
---
为什么选择 QT 作为项目开发的首选 IDE？

Qt 提供了所有必要的工具来设计、开发、构建和将应用部署在 Raspberry Pi 上。本教程主要介绍如何使用 Qt 工具的 GUI，在 Raspberry Pi 4 设备上开发 Linux 应用程序。

嵌入式系统通常是专门为特定任务设计的计算机系统，由于内嵌在
提出一个问题，在这个教程中，是否能够通过交叉编译使用诸如 PiGPIO 这种包？

该教程是基于 Ubuntu 系统中的 QT 和 Raspberry Pi 之间实现交叉编译。（这个地方需要组织一下语言）

在开始之前，有一些必要的组件
# 主机的设置
---
在主机上创建一些需要的文件夹，用来存放交叉编译的组件。这样做的目的是为了方便在将来使用交叉编译的过程中，需要用到的重要组件。
- Sysroot : 这个文件中存放的是主机内目标文件系统的缩小版本。所以，我们将其命名为 `rpi-sysroot`

```bash
cd ~
mkdir rpi-sysroot rpi-sysroot/usr rpi-sysroot/opt
mkdir qt-host qt-raspi qthost-build qtpi-build
```

# 设置 Raspberry Pi 
---
假设已经成功配置了 Raspberry Pi OS，并且进入了系统桌面。接下来，打开 **「终端」**，用命令行进行交叉编译的配置。

### 安装依赖
更新系统，并将软件库升级到最新版本。
```bash
sudo apt-get update
sudo apt full-upgrade
sudo reboot
```
接下来，安装包依赖。QT 需要这些库在 Raspberry Pi 中部署各种应用程序。
```bash
sudo apt-get install libboost-all-dev libudev-dev libinput-dev libts-dev 
sudo apt-get install libmtdev-dev libjpeg-dev libfontconfig1-dev libssl-dev 
sudo apt-get install libdbus-1-dev libglib2.0-dev libxkbcommon-dev libegl1-mesa-dev 
sudo apt-get install libgbm-dev libgles2-mesa-dev mesa-common-dev libasound2-dev 
sudo apt-get install libpulse-dev gstreamer1.0-omx libgstreamer1.0-dev 
sudo apt-get install libgstreamer-plugins-base1.0-dev  gstreamer1.0-alsa libvpx-dev 
sudo apt-get install libsrtp2-dev libsnappy-dev libnss3-dev "^libxcb.*" flex bison 
sudo apt-get install libxslt-dev ruby gperf libbz2-dev libcups2-dev libatkmm-1.6-dev 
sudo apt-get install libxi6 libxcomposite1 libfreetype6-dev 
sudo apt-get install libicu-dev libsqlite3-dev libxslt1-dev

sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libx11-dev 
sudo apt-get install freetds-dev libsqlite3-dev libpq-dev libiodbc2-dev firebird-dev 
sudo apt-get install libgst-dev libxext-dev libxcb1 libxcb1-dev libx11-xcb1 libx11-xcb-dev 
sudo apt-get install libxcb-keysyms1 libxcb-keysyms1-dev libxcb-image0 libxcb-image0-dev 
sudo apt-get install libxcb-shm0 libxcb-shm0-dev libxcb-icccm4 libxcb-icccm4-dev 
sudo apt-get install libxcb-sync1 libxcb-sync-dev libxcb-render-util0 libxcb-render-util0-dev 
sudo apt-get install libxcb-xfixes0-dev libxrender-dev libxcb-shape0-dev libxcb-randr0-dev 
sudo apt-get install libxcb-glx0-dev libxi-dev libdrm-dev 
sudo apt-get install libxcb-xinerama0 libxcb-xinerama0-dev libatspi2.0-dev libxcursor-dev 
sudo apt-get install libxcomposite-dev libxdamage-dev libxss-dev libxtst-dev 
sudo apt-get install libpci-dev libcap-dev libxrandr-dev 
sudo apt-get install libdirectfb-dev libaudio-dev libxkbcommon-x11-dev
```
还需要在 Raspberry Pi 中创建一个文件夹，用于存放针对 QT 的安装文件。
```bash
sudo mkdir /usr/local/qt6
```
# 设置主机
---
现在我们进行主机部分的设置，主机中使用的是 x86_64 架构的 Ubuntu 20.04 系统。理论上，该教程适用于任何 x86_64 架构的系统发行版。
### 更新系统
同样的，我们先更新 Ubuntu 系统中的软件包。
```bash
sudo apt update
sudo apt upgrade
```
### 安装 QT 依赖
接下来安装程序包依赖项。其中一些软件包是编译 Qt 6 所需的构建工具。
```bash
sudo apt-get install make build-essential libclang-dev ninja-build 
sudo apt-get install gcc git bison python3 gperf pkg-config libfontconfig1-dev 
sudo apt-get install libfreetype6-dev libx11-dev libx11-xcb-dev libxext-dev 
sudo apt-get install libxfixes-dev libxi-dev libxrender-dev libxcb1-dev 
sudo apt-get install libxcb-glx0-dev libxcb-keysyms1-dev libxcb-image0-dev 
sudo apt-get install libxcb-shm0-dev libxcb-icccm4-dev libxcb-sync-dev 
sudo apt-get install libxcb-xfixes0-dev libxcb-shape0-dev libxcb-randr0-dev 
sudo apt-get install libxcb-render-util0-dev libxcb-util-dev libxcb-xinerama0-dev 
sudo apt-get install libxcb-xkb-dev libxkbcommon-dev libxkbcommon-x11-dev 
sudo apt-get install libatspi2.0-dev libgl1-mesa-dev libglu1-mesa-dev freeglut3-dev
```
### 安装交叉编译器
接下来，我们需要获取交叉编译器。在本指南中，我们将从 Ubuntu/Debian 软件包存储库安装它，这是获取 ARM64 交叉编译器的最简单方法。
```bash
sudo apt install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu
```

# 设置 SSH 连接
---
在进行交叉编译的过程中，需要 Raspberry Pi 和主机之间进行 SSH 连接。这是在两个设备之间传输数据所必需的。