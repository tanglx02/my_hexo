---
title: 搭建邮箱服务器(postfix+dovecot)
categories:
  - Linux
  - 服务
tags:
  - Linux
  - Windows
  - 笔记
  - 技能比赛
  - 服务器
  - 邮箱
abbrlink: 4b62fc07
date: 2020-12-18 09:12:27
top:
---
## 一、准备工作
服务器centos
域名
## 二、postfix配置安装
### 1.0安装postfix
yum install postfix -y

### 2.0 配置文件修改
**编辑postfix 主配置文件，vi /etc/postfix/main.cf**
例如我的域名是：cloud.com ,邮件主机就是mail.cloud.com
(1)给 /etc/postfix/main.cf,做备份

``` xl
[root@cloud postfix]# cp /etc/postfix/main.cf /etc/postfix/main.cf.bak
```
(2)修改mail.cf中的myhostname
![](https://storage.freecplus.top/images/2020/12/20/20201220200615.png)
填主机名
(3)修改mail.cf中mydomail
![](https://storage.freecplus.top/images/2020/12/20/20201220200732.png)
填域名
(4)修改mail.cf中myorigin
![](https://storage.freecplus.top/images/2020/12/20/20201220201052.png)
(5)修改main.cf中smtp的监听端口

``` nix
inet_interfaces = localhost 注释掉，改为 inet_interfaces=all
```

![](https://storage.freecplus.top/images/2020/12/20/20201220201313.png)
(6)修改main.cf中inet_protocols
把all改成ipv4
![](https://storage.freecplus.top/images/2020/12/20/20201220201452.png)
(7)修改main.cf中的mydestination
mydestination参数设定能够将接受信件主机名称，Postfix预设只能收到hostname与domain name 以及本机端的信件，此步骤是再增加能收信件的网络名称
![](https://storage.freecplus.top/images/2020/12/20/20201220202001.png)
注释掉第一行，反注释第二行
(8)设定信任客户端 
mynetworks 参数设定信任的用户端，当要寄信时，会参考此值，若非信任的用户，则不会帮你的信件转到其它的MTA主机上。
![](https://storage.freecplus.top/images/2020/12/20/20201220202458.png)
参考第一行，这里我该成0.0.0.0/0
(9)设定relay_domain转发邮件域名
	规范可以relay的MTA主机位址（收发main的程序一般统称为邮件代理MUA(main user agent)）通常这个都直接设为mydestination
	![](https://storage.freecplus.top/images/2020/12/20/20201220202943.png)
(10)创建用户

``` groovy
useradd -s /sbin/nologin tonlx
mkdir -p /home/tonlx/mail/.imap/INBOX //给用户创建存储目录
chown -R tonlx /home/tonlx/mail //赋予权限
```
## 三、dovecot配置
看我另外一篇文章(sendmail+dovecot)
## 四、重启服务与关闭防火墙
[root@cloud postfix]# systemctl restart postfix.service  //重启postfix
[root@cloud mail]# systemctl restart dovecot.service 	重启dovecot
[root@cloud mail]# setenforce 0  //关闭selinux
[root@cloud mail]# systemctl stop firewalld  //关闭防火墙



