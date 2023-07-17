---
title: samba
categories:
  - 技能大赛
tags:
  - 技能大赛
abbrlink: d6bbfdfc
date: 2021-05-09 23:09:36
top:
---

## 

## samba服务配置

1.安装

`yum install samba -y`

2.创建用户

`useradd -s /sbin/nologin user1`   //创建user1用户

`useradd -s /sbin/nologin user2`  //创建user2用户

`useradd -s /sbin/nologin user3`  //创建user3用户

`smbpasswd -a user1`  //创建samba用户user1用户

`smbpasswd -a user2`  //创建samba用户user2用户

`smbpasswd -a user3`  //创建samba用户user3用户

3.创建本地目录

`mkdir -p /opt/a{1,2,3}` //创建目录分别为/opt/a1，/opt/a2，/opt/a3

`mkdir -p /opt/public`  //创建目录public

`chmod -R 777 /opt/` //赋予权限777

4.配置共享

`vim /etc/samba/smb.conf`   //进入samba的配置文件

![](https://storage.freecplus.top/images/2021/image-20210507193630186.png)

添加共享目录

## samba权限配置

1.创建用户组

`groupadd manager`

`usermod -G manager user1`

2.编辑samba配置文件

`vim /etc/samba/smb.conf`

`[staff1]  //共享名称`

`path = /opt/a1  // 共享路径`

`write list = user1 // 允许user1有写入权限`

`read list = user1  //使user1有读写权限`

`valid users = user1  //使user1对staff1有访问权限`

![](https://storage.freecplus.top/images/2021/image-20210507194239538.png)

3.用户映射

`vim /etc/samba/smb.conf`   //进入samba的配置文件

58 行左右加入

`username map = /etc/samba/smbusers` 用户映射文件

`vim /etc/samba/smbuser` //配置用户映射文件，加入以下内容

`user1= tony`

`user2 = tom`

4.测试登录

`yum install samba-client -y  //安装客户端`

`smbclient -L 10.100.100.102 -U tony` 查看user1的共享目录



## 限制上传文件

`vim /etc/samba/smb.conf	//编辑smb配置文件`

对需要限制的共享目录加入

`veto files = /*.exe/*.bmp/	//用来禁止上传可执行（.exe）及位图（.bmp）文件。`

`veto files = /*root*/	//用来禁止上传包含root关键字的文件或目录。`

