---
title: raid
categories:
  - 技能大赛
tags:
  - 技能大赛
abbrlink: 578763b3
date: 2021-05-09 23:09:36
top:
---

## 

## 一、添加RAID1添加热备盘

1.添加5块硬盘

2.创建基础阵列RAID1

``mdadm -C /dev/md1 -a yes -l 1 -n 2 /dev/sd[bc]  //sdc和sdc创建RAID1`

`mdadm -Ds > /dev/mdadm.conf`  //生成配置文件

3.制定计划任务

`crontab -e -u root`

`* 0 * * 5 /sbin/mdadm -a /dev/md1 /dev/sdd` //加入以下内容

## 二、条带卷的建立

1.磁盘分区

`fdisk /dev/sde`  //对/dev/sde磁盘进行操作，创建3个100M的主分区，在将第3个分区改为逻辑分区(8e)

2.建立条带卷

`mdadm -C /dev/md1 -a yes -l 0 -n 3 -c 8 /dev/sde[123]`

`mdadm -Ds > /dec/mdadm.conf`  // 生成配置文件





## 三、建立lvm简单卷



