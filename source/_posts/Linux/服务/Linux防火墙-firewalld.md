---
title: Linux防火墙-firewalld
categories:
  - Linux
  - 服务
tags:
  - Linux
  - 服务
  - firewalld
  - 防火墙
abbrlink: abd795e0
date: 2021-04-12 14:46:22
top:
---

# Linux防火墙-firewalld
自centos7以后的Linux版本，firewalld工具已经取代iptables工具，在Linux中防火墙工具只是一个工具，而firewalld服务只是将配置好的服务交给内核层面的nftables包过滤框架来处理。
相对于传统的Linux防火墙，firewalld引入了zone，即区域的概念，不同的区域适用于不同的环境，可以随时切换区域。
## 防火墙查看命令
1）查看防火墙版本

``` dockerfile
firewall-cmd --version
```
2）查看防火墙状态

``` dockerfile
firewall-cmd --state
```

3）查看防火墙全部信息

``` vim
firewall-cmd --list-all
```
4）查看防火墙已打开端口

``` dockerfile
firewall-cmd --list-port
```
5）查看防火墙已打开服务

``` thrift
firewall-cmd --list-service
```
6）查看防护墙预定义服务

``` dockerfile
firewall-cmd --get-services
```

7）查看防火墙可用区域

``` dockerfile
firewall-cmd --get-zones
```
8）查看防护墙正在使用的区域

``` vbscript
firewall-cmd --get-default-zone
```

## 防火墙配置策略
1）设置默认使用区域

``` vbscript
firewall-cmd --set-default-zone=<区域名称>
```

2）开放、移去某个端口。
开放80端口

``` jboss-cli
firewall-cmd --zone=public --add-port=80/tcp --permanent
```

移去80端口

``` jboss-cli
firewall-cmd --zone=public --remove-port=80/tcp --permanent
```

3）开放、移去范围端口。

开放5000-5500之间的端口

``` jboss-cli
firewall-cmd --zone=public --add-port=5000-5500/tcp --permanent
```

移去5000-5500之间的端口

``` jboss-cli
firewall-cmd --zone=public --remove-port=5000-5500/tcp --permanent
```

4）开放、移去服务。
 开放ftp服务

``` jboss-cli
firewall-cmd --zone=public --add-service=ftp --permanent
```

移去http服务

``` jboss-cli
firewall-cmd --zone=public --remove-service=ftp --permanent
```

5）重新加载防火墙配置（修改配置后要重新加载防火墙配置或重启防火墙服务）。

``` dockerfile
firewall-cmd --reload
```

6）设置开机时启用、禁用防火墙服务。
启用服务

``` bash
systemctl enable firewalld
```

禁用服务

``` bash
systemctl disable firewalld
```


