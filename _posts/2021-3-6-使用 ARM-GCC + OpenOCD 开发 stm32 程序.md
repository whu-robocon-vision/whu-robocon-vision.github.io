# 使用 ARM-GCC + OpenOCD 开发 stm32 程序

对于习惯了现代编译环境的人来说，可能 keil 的用户界面体验和新鲜感比较差。这篇文章介绍了如何利用ARM-GCC 对 arm 嵌入式设备开发和利用 OpenOCD 进行下载和调试。

![image-20210307190949546](https://i.loli.net/2021/03/23/kIlmRBz7LYwaPJA.png)

## arm-none-eabi-gcc

```ARM architecture，no vendor，not target an operating system，complies with the ARM EABI```

Arm官方用于编译 ARM 架构的裸机系统（包括 ARM Linux 的 boot、kernel，**不适用编译 Linux应用**），一般适合 ARM7、Cortex-M 和 Cortex-R 内核的芯片使用，所以不支持那些跟操作系统关系密切的函数，比如fork(2)，他使用的是 newlib 这个专用于嵌入式系统的C库。

1. 从[官网	](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)下载 arm-none-eabi-gcc，不同的平台可以选择不同的安装包，linux 也可以通过命令安装

   ```shell
   sudo apt-get install arm-none-eabi-gcc
   ```

2. 安装

3. 配置环境变量

   ![image-20210307194130795](https://i.loli.net/2021/03/23/Zq7nfhIXCBy1NMK.png)

4. 测试

   ![image-20210307194234812](https://i.loli.net/2021/03/23/MFYQwroVpCX4WRI.png)

# OpenOCD

![image-20210307192432913](https://i.loli.net/2021/03/23/2PI9xcXbp6t5ogV.png)

[OpenOCD](http://openocd.org/)是一个运行于PC上的开源调试软件，它可以控制包括Wiggler之内的很多JTAG硬件；我们可以将它理解为一种GDB服务程序。最初是由Dominic Rath同学还在大学期间发起的（2005年）项目。OpenOCD旨在提供针对嵌入式设备的调试、系统编程和边界扫描功能。OpenOCD的功能是在仿真器的辅助下完成的，仿真器是能够提供调试目标的电信号的小型硬件单元。仿真器是必须的，因为调试主机（运行OpenOCD的主机）通常不具备这种电信号的直接解析功能。

1. 下载

   OpenOCD 只能通过源码编译安装，可以下载其他开发者编译好的版本。

   windows可以在[这里](https://gnutoolchains.com/arm-eabi/openocd/)下载

2. 安装

3. 设置环境变量

4. 测试

# Zadig

[Zadig](https://zadig.akeo.ie/) is a Windows application that installs generic USB drivers, such as [WinUSB](https://docs.microsoft.com/en-us/windows-hardware/drivers/usbcon/winusb), [libusb-win32/libusb0.sys](https://sourceforge.net/p/libusb-win32/wiki/Home/) or [libusbK](http://libusbk.sourceforge.net/UsbK3/), to help you access USB devices.

![image-20210307194444917](https://i.loli.net/2021/03/23/zH9rb4VUZus53iD.png)