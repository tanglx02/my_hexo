---
title: centos单网卡多ip
categories:
  - Linux
  - 折腾
tags:
  - Linux
  - 服务
  - 折腾
  - 网卡
abbrlink: 65433eb7
date: 2021-05-01 11:02:37
top:
---


``` groovy
centos单网卡多IP
vi /etc/sysconfig/network-script/[网卡名称]
```

``` makefile
修改内置参数
BOOTPROTO=static
ONBOOT=yes
```

![](https://storage.freecplus.top/images/2021/20210501110616.png)

``` lsl
网卡一
IPADDR=192.168.10.121
PERFIX=24
GATEWAT=192.168.10.254
网卡二
IPADDR2=192.168.10.121
PERFIX2=24
GATEWAT2=192.168.10.254
....
依次类推
最后写上DNS服务器即可
DNS1=192.168.10.101
```