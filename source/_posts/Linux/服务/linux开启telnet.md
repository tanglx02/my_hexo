---
title: linux开启telnet
categories:
  - Linux
  - 服务
tags:
  - Linux
  - 服务
  - telnet
abbrlink: da04133f
date: 2021-04-27 14:19:30
top:
---
# Centos6启telnet
安装

``` elixir
[root@ntp1 ~]# yum install telnet telnet-server xinetd
```
开启xinetd自启动和启动xinetd

``` elixir
[root@ntp1 ~]# chkconfig xinetd on
[root@ntp1 ~]# service xinetd restart
```
允许root用户登录

``` elixir
[root@ntp1 ~]# vi /etc/pam.d/remote 
```
![](https://storage.freecplus.top/images/2021/20210428110302.png)
修改/etc/pam.d/remote，注释掉：auth required pam_securetty.so

如果要做相关的配置可参考模板

``` stata
cat /usr/share/doc/xinetd-2.3.14/sample.conf 
```

## 相关文章

## Cetnos7开启telnet
安装

``` elixir
[root@ntp1 ~]# yum install telnet telnet-server xinetd
```
开启xinetd自启动和启动xinetd

``` elixir
[root@ntp1 ~]# systemctl enable xinetd
[root@ntp1 ~]# systemctl start xinetd
```

建立telnet文件

``` nix
[root@tonlx ~]# vi /etc/xinetd.d/telnet 
加入以下内容

service telnet
{
 flags           = REUSE
 socket_type     = stream
 wait            = no
 user            = root
 server          =/usr/sbin/in.telnetd
 log_on_failure  += USERID
disable         = no
}
```

