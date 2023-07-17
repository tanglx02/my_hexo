---
title: mdadm创建RAID以及定时备份
categories:
  - Linux
  - 服务
tags:
  - Linux
  - 服务
  - RAID
  - crontab
  - mdadm
abbrlink: c952ec28
date: 2021-05-05 11:52:05
top:
---


创建RAID1

``` elixir
[root@server1 ~]# mdadm -Cv /dev/md0 -a yes -l 1 -n 2 /dev/sd[b,c]
```

设置某周5晚24点开始把第三块硬盘加入备份

``` dts
[root@server1 ~]# crontab -e
加入以下内容，备份时间为5小时
* 0 * * 5 /sbin/mdadm /dev/md0 -a /dev/sdd  加入到md0中
* 5 * * 5 /sbin/mdadm /dev/md0 -r /dev/sdd  移除
```