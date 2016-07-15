---
layout: post
title: 解决U盘装系统提示加载驱动程序问题
categories: windows 
excerpt: U盘 装系统 驱动
comments: true
---
**如今安装系统用光驱的人肯定不多，一般最简单的方法就是通过U盘来安装系统。**

**以windows 7为例，在实际操作过程中，会碰到一个比较麻烦的问题...**

     加载驱动程序
         缺少所需的CD/DVD驱动器设备驱动程序。如果您具有软盘、CD、DVD，或USB闪存驱动器的驱动程序，请立即插入！...(后面省略)

看到这个窗口出现，我们下意识就听从微软的提示了：就是缺少驱动了。其实不然，这个提示误导了我们...

**分析与解决：**

- 此时或者返回上步安装界面,同时按下Shift+F10,会调出命令窗口:

- 键入 diskpart 查看磁盘,就会进入

       DISKPART>

- 继续键入list disk

      DISKPART> list disk 

      磁盘 ###  状态           大小     可用     Dyn  Gpt
      --------  -------------  -------  -------  ---  ---
      磁盘 0    联机              298 GB  5120 KB
      磁盘 1    无介质                0 B      0 B

可以发现并没有我们的u盘...

我们知道windws 7系统的安装其实就是先加载一个WIN7 PE的系统来引导安装的，而这个PE系统是WINDOWS7的内核，并且我们用U盘引导成功，他没有可能不认U盘，原因可能就出现在USB的U盘在PE系统中的识别上的驱动问题了。

- 重新插拔下U盘，然后可以再次检查下，就可以发现了。
      
      DISKPART> list disk

      磁盘 ###  状态           大小     可用     Dyn  Gpt
      --------  -------------  -------  -------  ---  ---
      磁盘 0    联机              298 GB  5120 KB
      磁盘 1    无介质                0 B      0 B
      磁盘 2    联机               28 GB      0 B

`注意：如果U盘插在usb3.0接口时仍然可能无法识别，此时就必须把U盘插在usb2.0接口上。`