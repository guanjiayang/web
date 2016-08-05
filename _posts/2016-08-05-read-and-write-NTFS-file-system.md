---
layout: post
title: mac电脑：一句话直接读写ntfs分区
categories: ntfs
excerpt: mac os rw
comments: true
---

相信强迫症的朋友不少，希望在MAC电脑中读写NTFS分区，但是却不想安装第三方工具...

- 打开你的磁盘工具，找到对应磁盘的通用唯一标识信息，记录下来。

- 打开终端

        `计算机名`:~ `用户名`$ 
        `计算机名`:~ `用户名`$ sudo su
        Password:                     （输入用户登录密码）
        sh-3.2# nano /etc/fstab
        
        GUN nano 2.0.6        File: /etc/fstab
        UUID=`复制你记录的唯一标识` none ntfs rw,auto
        
- 按control+x后按Y保存

- 重启你的电脑后打开find就能直接操作了
