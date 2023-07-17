---
title: centos搭建时间服务器
categories:
  - Linux
  - 服务
tags:
  - Linux
  - 服务
abbrlink: 39e8414f
date: 2021-04-27 09:09:49
top:
---

## 搭建chronyd服务
服务端

``` vim
yum install -y chrony  //安装ntp服务
firewall-cmd --zone=public --add-service=ntp --permanent  //开放ntp
systemctl restart firewalld  //重启防火墙
vi /etc/chrony.conf  //编辑chronyd服务的配置文件

```
![](https://storage.freecplus.top/images/2021/20210427091447.png)
第一部分：允许那个网段的ip获取时间
第二部分：单网路时间不可用时，采用本地时间

``` maxima
systemctl restart chronyd //重启服务
```

客户端

``` vim
yum install -y chrony  //安装ntp服务
firewall-cmd --zone=public --add-service=ntp --permanent  //开放ntp
systemctl restart firewalld  //重启防火墙
vi /etc/chrony.conf  //编辑chronyd服务的配置文件

```
![](https://storage.freecplus.top/images/2021/20210427091855.png)
采用192.168.10.200 这台服务器同步时间，iburst是优先

``` maxima
systemctl restart chronyd  //重启chronyd服务
chronyc sources //查看同步信息
```
![](https://storage.freecplus.top/images/2021/20210427092236.png)