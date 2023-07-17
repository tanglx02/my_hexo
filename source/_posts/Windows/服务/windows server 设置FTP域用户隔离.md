---
title: windows server 设置FTP域用户隔离
categories:
  - Windows
  - 服务
tags:
  - FTP
  - Windows
  - 域
abbrlink: e96c0ece
date: 2021-04-21 15:38:34
top:
---
## 一、实验环境
三台设备
2012 域控制器 ip 192.168.10.101
2008r2 FTP服务器 ip 192.168.10.104
win10 客户机 ip 192.168.10.107
实验说明
 1. 将FTP服务器加入域控制器中，其完全域名为ftp.2021skills. com
 2. 建立ftp 站点ftp.2021kils.com站点主目录为 C:\ftp,不允许匿名登录，所有用户只具有读取和写入文件权限，FTP站点欢迎消息为:“欢迎访问网络搭建FTP服务器!”，并且用命令浏览文件时使用UNIX方式显示，日志文件记录到 C: \\\ftp\LogFiles目录下;
 3. 为ftp1.2020skills.com设置域用户隔离，在域控制器中创建域用户ftpuser1和ftpuser2,密码为2020skills. com,设置两个用户主目录分别为网络文件夹\\\ftp\ftpuser1、\\\ftp\ftpuser2。
## 二、实验部署
1.在域控制器中添加用户，用户组，组织单元
![](https://storage.freecplus.top/images/2021/20210421155232.png)
2.在FTP服务器根目录中添加FTP的目录，与用户目录，并在各个目录中做好标记
![](https://storage.freecplus.top/images/2021/20210421155526.png)
![](https://storage.freecplus.top/images/2021/20210421155810.png)
3.建立站点ftp.2021skills. com，

``` x86asm
这里我填写主机名最后无法访问，尝试只是用ip最后成功
```

![](https://storage.freecplus.top/images/2021/20210421160119.png)
4.不允许匿名登录，所有用户具有写入和读取权限


![](https://storage.freecplus.top/images/2021/20210421160226.png)
5.设置欢迎消息
![](https://storage.freecplus.top/images/2021/20210421160512.png)
6.设置用命令浏览文件时使用UNIX方式显示
![](https://storage.freecplus.top/images/2021/20210421160631.png)
7.文件记录到C:\ftp\logfiles目录下
![](https://storage.freecplus.top/images/2021/20210421160812.png)
8.将FTP服务器根目录共享并设置权限给用户组
``` livecodeserver
这里的共享权限只给到域中的ftp组即可，防止samba访问越权
```
![](https://storage.freecplus.top/images/2021/20210421161255.png)
9.回到域控制器中的域用户管理点击查看-高级功能
![](https://storage.freecplus.top/images/2021/20210421161617.png)
10.选择用户-属性-属性编辑器修改msIIS-FTPRoot和msIIS-FTPDir

``` nix
注意：msIIS-FTPRoot=FTP根目录=ADFTProot、msIIS-FTPDir=用户主目录=用户名目录
```

![](https://storage.freecplus.top/images/2021/20210421161806.png)
11.在FTP服务器中打开用户隔离
![](https://storage.freecplus.top/images/2021/20210421162923.png)
12.到win10客户端检测
![](https://storage.freecplus.top/images/2021/20210421162828.png)
![](https://storage.freecplus.top/images/2021/20210421163059.png)
这里可以看到，ftp不但做到了隔离同样具有写入权限
![](https://storage.freecplus.top/images/2021/20210421164122.png)
如果试图通过samba访问则无法成功
![](https://storage.freecplus.top/images/2021/20210421164244.png)