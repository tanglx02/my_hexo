---
title: centos7开启ssh
categories:
  - Linux
  - 命令
tags:
  - centos7
  - 命令
  - ssh
abbrlink: ed0c47a3
date: 2020-12-04 15:16:16
top:
---
开启centos7，确保自己的openssh-server已经安装
## 一、安装openssh

``` elixir
[root@cloudhost7 ~]# yum install -y openssh-serever
```

![](https://storage.freecplus.top/images/2020/12/04/20201204152735.png)
## 二、把监听端口和监听地址等打开

``` elixir
[root@cloudhost7 ~]# vi /etc/ssh/sshd_config 
```
注释掉这几行前面的#

``` css
Port 22    //监听端口
ListenAddress 0.0.0.0 //监听地址
istenAddress ::
PermitRootLogin yes  //允许远程登陆
PasswordAuthentication yes //使用用户名密码来作为连接验证
```

![](https://storage.freecplus.top/images/2020/12/04/20201204152943.png)

## 三、 开启  sshd  服务
输入 

``` elixir
[root@cloudhost7 ~]# sudo service sshd start
```
## 四、设置开机自启动sshd

``` elixir
[root@cloudhost7 ~]# systemctl enable sshd.service
```






