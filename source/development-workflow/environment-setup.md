---
title: Software Environment Setup Guide
date: 2019-06-17
version: 3.8.1
keywords: [hardware setup，M100 UART Connector, A3 UART Connector, N3 UART]
---

This guide details the software environment needed to work with the Onboard SDK. 

## All Platforms

#### Download the SDK and Required Tools

- <a href="https://github.com/dji-sdk/Onboard-SDK" target="_blank">Download</a> the onboard SDK repository from Github
- <a href="https://www.dji.com/product/matrice600/info#downloads" target="_blank">Download</a> the DJI PC Assistant 2 software for Windows/Mac
- <a href="http://www.dji.com/product/goapp" target="_blank">Download</a> the DJI GO App to your mobile device

#### Update Firmware

- Connect your computer to the Micro-USB port on the M100/600 or A3/N3. For the M210, use the USB-A to USB-A cable provided with the aircraft.
- Update your aircraft/flight controller with the latest released firmware. Please visit the [Compatibility Matrix](../appendix/versioning.html) to find out which SDK version your firmware supports.

#### Enable OSDK API

The OSDK API needs to be enabled to allow communication between the onboard computer and the aircraft or flight controller.

- With your aircraft/flight controller connected to your PC/Mac, launch DJI Assistant 2 and check the box marked `Enable API Control` on the `SDK` page.

![Enable API Control](../images/common/N1UI.png)

#### Onboard SDK Application Registration

- You must register as a developer with DJI and create an OSDK application ID and Key pair. Please go to <a href="https://developer.dji.com/user/apps/#onboard" target="_blank">https://developer.dji.com/user/apps/#onboard</a> to complete registration.
- After registration, you need to create the APP to get APP ID and Key in the developer center.

![Enable API Control](../images/common/APP_ID.png)

#### Flight Platform Activation

Each new vehicle or flight controller must be activated the first time it is used with an OSDK application. 

The OSDK provides APIs for this activation, and all OSDK samples implement the activation. So you can run the OSDK sample to activate the drone

When you activate the drone, please open DJI GO or DJI Assistant 2.

## Ubuntu Linux

##### Toolchain

To build standalone Linux applications based on the OSDK, you need:

* A supported C++ compiler - currently only GCC (Tested with gcc 4.8.1/5.3.1)
* A bash shell
* CMake >= 2.8
* A modern Linux distribution
* (Optional) Libusb library for [Advanced Sensing](../sample-doc/advanced-sensing-stereo-images.html) feature on M210

##### Permissions

You need to add your user to the `dialout` group to obtain read/write permissions for the uart communication; follow these steps to do so:

1. Type `sudo usermod -a -G dialout $USER` in a terminal
2. Log out of your user account and log in again for the permissions to take effect.

For M210 users interested in the [Advanced Sensing](../sample-doc/advanced-sensing-stereo-images.html) feature, you will need to add an udev file to allow your system to obtain permission and to identify DJI USB port. 

1. Create a udev file called `DJIDevice.rules` inside `/etc/udev/rules.d/`
2. Add `SUBSYSTEM=="usb", ATTRS{idVendor}=="2ca3", MODE="0666"` to this file
3. Reboot your computer

To make sure your Linux environment is ready to run OSDK applications, follow the [Linux Platform Guide](../development-workflow/sample-setup.html#linux-onboard-computer) on the Sample Setup page and run a sample app.

## STM32

##### Introduction

The system has the following setup:
![system diagram](../images/STM32/STM32_System_Structure.png)

The user can view the output of the program through the USART2 port of the STM32. The app communicates with the DJI product connected to the USART3 port through the Onboard SDK and prints feedback/debug information to the user thorugh USART2.

##### Toolchain Requirements
- Keil MDK > 5.22 (armcc 5.06)
- Windows PC to run Keil

##### Toolchain Setup

- Configure the USART3 port to a baudrate of 230400 in your sample app
- To download (flash) the App binary to the STM32 board, connect the PC to the STM32's "mini-USB" port.
- In order for Keil to build code for the target board, you need to use Keil's `Pack Installer` to install the latest STM32F4xx_DFP.2.x.x pack, as shown below.
- Alternatively, you can download manually from <a href="http://www.keil.com/dd2/Pack/" target="_blank">http://www.keil.com/dd2/Pack/</a> and import the downloaded file from Pack Installer.)

![Keil_PackInstall](../images/STM32/STM32_Keil_PackInstall.png)

To make sure your STM32 environment is ready to run OSDK applications, follow the [STM32 Platform Guide](../development-workflow/sample-setup.html#stm32-onboard-computer) on the Sample Setup page and run a sample app.

## Linux with ROS

##### Software Requirements:

* Install C, C++ Compiler and Development Tools by installing ``build-essential``
* Install CMake 2.8.3 or newer
* <a href="http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment">Install ROS and its dependencies</a>
* Operating System: Ubuntu 16.04 (x86/ARM)
* ROS version: ROS Kinetic

##### Toolchain Setup

* If you don't have a catkin workspace, create one as follows:
```
mkdir catkin_ws
cd catkin_ws
mkdir src
cd src
catkin_init_workspace
```
* What should be emphasized is that the baudrate between the ROS device and the drone OSDK uart should be greater than 921600. Because many subscription topics are subscribed by ROS by default and they need more communication bandwidth.
* If you are using the ttyTHS2 of Manifold 2-G to communicate with the drone, the baudrate is recommended as 1000000 but not 921600. Because the baudrate 921600 of Manifold 2-G have a little deviation from the actual value. You can ref to the [Manifold 2 User Guide] for more details.(https://dl.djicdn.com/downloads/manifold-2/20190528/Manifold_2_User_Guide_v1.0_EN.pdf)

##### Permissions

You need to add your user to the `dialout` group to obtain read/write permissions for the uart communication; follow these steps to do so:

1. Type `sudo usermod -a -G dialout $USER` in a terminal
2. Log out of your user account and log in again for the permissions to take effect.

For M210 users interested in the [Advanced Sensing](../sample-doc/advanced-sensing-stereo-images.html) feature, you need to add an udev file to allow your system to obtain permission and identify DJI USB port. 

1. Create a udev file called `DJIDevice.rules` inside `/etc/udev/rules.d/`
2. Add `SUBSYSTEM=="usb", ATTRS{idVendor}=="2ca3", MODE="0666"` to this file
3. Reboot your computer

To make sure your ROS environment is ready to run OSDK applications, follow the [ROS Platform Guide](../development-workflow/sample-setup.html#ros-onboard-computer) on the Sample Setup page and run a sample app.

## Qt

##### Toolchain Requirements

- Qt [5.9 or newer](https://info.qt.io/download-qt-for-application-development) (You may choose the Open-Source option)
- Qt Creator 4.3 (Part of the download package above)
- MSVC2015/ MSVC2013/ MinGW 5.3 (Windows 10) *OR*
- Gcc 5.3.1 (Ubuntu Linux) *OR*
- Apple LLVM 7.0 or newer (MacOS)

The application may also work on other platforms/compilers but has not been tested with any combinations other than these.