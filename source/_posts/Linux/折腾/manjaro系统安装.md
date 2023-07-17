---
title: manjaro系统安装
categories:
  - Linux
  - 折腾
tags:
  - Linux
  - 折腾
  - manjaro
abbrlink: 4ebd2aa1
date: 2021-05-31 10:23:00
top:
---

这里我是用的桌面版本是xfce，我喜欢它的风格
## 一、更换源
1.更换pacman的源为国内源

``` stylus
sudo pacman-mirrors -i -c China -m rank
```

![](https://storage-cn.github.io/images/2021/20210531150413.png)

2.同步刷新本地软件数据库

``` ebnf
sudo pacman -Syy
```
3.如果你使用的vm虚拟机你可能需要安装一下vm-tools

``` vim
克隆安装脚本
git clone https://github.com/rasa/vmware-tools-patches.git
进入目录
cd vmware-tools-patches
执行安装脚本
sudo ./patched-open-vm-tools.sh
```
4.添加archlinux ARU源
vim /etc/pacman.conf

``` ini
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```
5.安装yay

``` ebnf
sudo pacman -S yay
```

6.安装密钥

``` ebnf
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring
```
## 二、安装必备软件
### 安装输入法
 

``` nginx
sudo pacman -S fcitx-im    #默认全部安装
 sudo pacman -S fcitx-configtool
 sudo pacman -S fcitx-sogoupinyin #如果用不了pacman，试试yay
 sudo pacman -S fcitx-googlepinyin #也可以安装google输入法
```

 新建~/.xprofile文件，加入如下内容

``` bash
 export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```