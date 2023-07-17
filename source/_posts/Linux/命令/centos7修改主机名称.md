---
title: centos7修改主机名称
categories:
  - Linux
  - 命令
tags:
  - centos7
  - 命令
abbrlink: 779dde11
date: 2020-12-04 14:42:47
top:
---
修改centos7主机名称
我是用的是vi编辑器，也可以是nano
## 一、以root方式登陆
![](https://storage.freecplus.top/images/2020/12/04/20201204150021.png)
## 二、输入hostname可查看名称

![](https://storage.freecplus.top/images/2020/12/04/20201204150142.png)
## 输入vi /etc/hostname修改名称
![](https://storage.freecplus.top/images/2020/12/04/20201204150245.png)
这里我给它修改为cloudhost7
## 输入vi /etc/hosts 修改网络名
![](https://storage.freecplus.top/images/2020/12/04/20201204150535.png)
修改括号中的部分
![](https://storage.freecplus.top/images/2020/12/04/20201204150615.png)