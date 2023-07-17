---
title: 虚拟机克隆后无法使用网卡-centos
categories:
  - Linux
  - 折腾
tags:
  - Linux
  - 问题
  - 折腾
abbrlink: 441c9188
date: 2021-04-19 10:17:59
top:
---


# 虚拟机克隆后无法使用网卡-centos
## 一、centos6解决方法
 删除HAWADDR和UUID

``` groovy
 sed -i '/UUID/d' /etc/sysconfig/network-scripts/ifcfg-eth0
sed -i '/HWADDR/d' /etc/sysconfig/network-scripts/ifcfg-eth0
```
清除网卡相关信息
``` elixir
 > /etc/udev/rules.d/70-persistent-net.rules
```
重启
``` ebnf
reboot
```

![](https://storage.freecplus.top//images/2021/20210419102030.png)