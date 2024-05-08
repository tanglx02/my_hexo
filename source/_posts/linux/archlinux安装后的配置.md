---
title: archlinux安装后的配置
date: 2024-04-24 23:11:24
categories: 
- linux
tags: 
- linux
- archlinux
top: 
---
[toc]
# 一、系统配置
## 1.创建普通用户
创建用户tanglx，并加入到wheel组

``` ebnf
useradd -m -G wheel tanglx
```
修改密码

``` ebnf
passwd tanglx
```
提升权限
编辑 /etc/sudoers，找到#%wheel ALL=(ALL:ALL) ALL，取消#号

``` pgsql
%wheel ALL=(ALL:ALL) ALL
```

## 2.设置系统源并更新系统
安装自动设置源

``` ebnf
sudo pacman -Sy reflector
```
设置自动选择源
``` css
reflector -p https -c China --delay 3 --completion-percent 95 --sort rate --save /etc/pacman.d/mirrorlist

```
编辑 sudo vim /etc/pacman.conf ，末尾加入
``` ini
[archlinuxcn]
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```



更新系统

``` ruby
sudo pacman -Syyu
pacman-key --init
pacman-key --populate
sudo pacman -S archlinuxcn-keyring
```
如果安装archlinuxcn-keying报错

``` javascript
请使用以下命令在本地信任 farseerfc 的 key 。此 key 已随 archlinux-keyring 安装在系统中，只是缺乏信任：

sudo pacman-key --lsign-key "farseerfc@archlinux.org"
之后继续安装 archlinuxcn-keyring ：

sudo pacman -S archlinuxcn-keyring
```
再次更新

``` ebnf
sudo pacman -Syyu
```

## 3.安装aur助手
base-devel编译时候用到的工具
``` ebnf
pacman -S base-devel yay
```

## 4.显卡驱动安装
****切记如果要装kde环境直接跳过显卡安装环节，否则会报错
我的cpu为i5 4590 显卡NVIDIA gt 730，其它显卡参考下面链接修改
https://zhuanlan.zhihu.com/p/568981775
安装inter核显驱动

``` ebnf
pacman -S mesa vulkan-intel  
```
安装NVIDIA独显卡驱动

``` tcl
sudo pacman -S nvidia-open nvidia-settings lib32-nvidia-utils 
yay -S nvidia-470xx-dkms
```
      
编辑 /etc/mkinitcpio.conf，从 HOOKS 数组中去掉 kms

``` ini
HOOKS=(... kms ...)  # 请去掉 kms
```
重新生成 initramfs
``` ebnf
mkinitcpio -P
```
其次，编辑 /etc/default/grub，在 GRUB_CMDLINE_LINUX_DEFAULT 中添加“nvidia_drm.modeset=1”。

``` ini
GRUB_CMDLINE_LINUX_DEFAULT="... nvidia_drm.modeset=1"
```

然后重新生成 grub 配置

``` gradle
grub-mkconfig -o /boot/grub/grub.cfg
```

## 5.其它驱动
如果是amd执行 pacman -S amd-ucode
``` ebnf
pacman -S intel-ucode
```

## 6.安装桌面环境
字体安装

``` gauss
pacman -S noto-fonts noto-fonts-cjk noto-fonts-emoji
```
桌面安装
目前kde使用最新的plasma，plasma-wayland-session不在使用

``` ebnf
pacman -S xorg plasma kde-applications
```
设置窗口管理器开机自启动
``` routeros
systemctl enable sddm.service
```

## 7.输入法安装
//安装小企鹅输入法

``` vim
sudo pacman -S fcitx5 fcitx5-qt fcitx5-gtk fcitx5-lua kcm-fcitx5
```
安装完成以后配置一下*.xprofile* 文件，终端输入：

``` bash
sudo vim ~/.xprofile
```
添加

``` routeros
export INPUT_METHOD=fcitx5
export GTK_IM_MODULE=fcitx5
export QT_IM_MODULE=fcitx5
export XMODIFIERS=@im=fcitx5
```
fcitx5中文词库

``` nginx
sudo pacman -S fcitx5-pinyin-zhwiki rime-pinyin-zhwiki fcitx5-pinyin-moegirl-rime
```
fcitx5输入语言
``` awk

//中文
sudo pacman -S fcitx5-chewing fcitx5-rime fcitx5-chinese-addons 
//日语
sudo pacman -S fcitx5-anthy fcitx5-kkc fcitx5-skk fcitx5-mozc 
//韩语
sudo pacman -S fcitx5-hangul
//越南语
sudo pacman -S fcitx5-unikey fcitx5-bamboo 
```

配置 /etc/environment 

``` gradle
sudo vim /etc/environment 
```

添加

``` routeros
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
GLFW_IM_MODULE=ibus
```

