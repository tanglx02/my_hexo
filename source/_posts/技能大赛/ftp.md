---
title: ftp
categories:
  - 技能大赛
tags:
  - 技能大赛
abbrlink: a84da34e
date: 2021-05-09 23:09:36
top:
---

## 安装ftp服务并建立站点

1.网卡配置

`yum install vsftpd -y`	//安装vsftpd

`cd /etc/sysconfig/network-scripts/`

`cp ifcfg-eth0 ifcfg-eth0:0`	//建立网卡二

`cp ifcfg-eth0 ifcfg-eth0:1`	//建立网卡三

2.站点复制多个站点

`cd /etc/vsftpd`

`cp vsftpd.conf vsftpd1.conf`

`cp vsftpd.conf vsftpd2.conf`

3.修改监听网卡

`vim vsftpd.conf`

`listen_address=10.100.100.105`

`vim vsftpd1.conf`

`listen_address=10.100.100.106`

`vim vsftpd2.conf`

`listen_address=10.100.100.107`

4.站点配置

`mkdir /var/ftp{1,2}`

`local_root=/var/ftp1 //定义vsftpd1.conf的主目录`

`local_root=/var/ftp2 //定义vsftpd2.conf的主目录`

## ftp chroot设置

知识拓展

    chroot_local_user #是否将所有用户限制在主目录
    
    chroot_list_enable #是否启动限制用户的名单 YES为启用  NO禁用(包括注释掉也为禁用)
    
    chroot_list_file=/etc/vsftpd/chroot_list #是否限制在主目录下的用户名单
    				chroot_list_enable和chroot_list_file 配合使用
## 

## ftp用户同主目录

`1.建立两个用户并指定同目录`

`useradd -d /ftp ftpuser3`

`useradd -d /ftp ftpuser4`

`chmod 777 /ftp	//赋予权限`

## ftp根目录

设置根目录后，用户目录将失效

local_root = /ftp 	//加入根目录

## ftp连接

Max_clients=200 （FTP的最大连接数）

Max_per_ip=4 （每IP的最大连接数）

/usr/share/doc/vsftpd-2.2.2/FAQ 文档里面有详细说明

