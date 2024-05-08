---
title: 物理机安装archLinux
date: 2024-04-24 21:12:04
categories: 
- linux
tags: 
- linux
- archlinux
top: 
---
[toc]
从官网下载镜像并通过up启动成功联网后
# 一、基础配置
## 1.设置时间
查看时间

``` maxima
timedatectl status 
```

如果时间不对

``` dsconfig
timedatectl set-ntp true  
```

如果时区不对

``` dsconfig
timedatectl set-timezone Asia/Shanghai
```
## 2.磁盘分区
对于 UEFI 需要至少创建三个分区（efi、swap、根）
![enter description here](https://picture.tanglx.cn/web/2024/1713970603396.png)
**格式化分区**
根分区

``` gradle
 mkfs.ext4 /dev/sda3 
```

交换分区

``` gradle
mkswap /dev/sda2
```

efi分区

``` gradle
mkfs.fat -F 32 /dev/sda1
```

lsblk -f 查看是否格式化分区类型成功
 ## 3.挂载分区
 *注意：挂载需要遵循一定的顺序，要先挂载根分区。*
根分区
``` bash
 mount /dev/sda3 /mnt
```
swap分区
``` gradle
 swapon /dev/sda2
```
efi分区
``` gradle
 mount --mkdir /dev/sda1 /mnt/boot
```

## 4.自动设置镜像源

``` css
reflector -p https -c China --delay 3 --completion-percent 95 --sort rate --save /etc/pacman.d/mirrorlist
```
## 5.安装基础包

``` bash
pacstrap -K /mnt base base-devel linux linux-firmware
```
## 6.设置fstab

``` gradle
genfstab -U /mnt >> /mnt/etc/fstab
```
# 一、切换到新系统

``` bash
arch-chroot /mnt
```
## 1.设置时区

``` gradle
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc
```
## 2.设置locale
安装编辑器和终端字体
``` vim
pacman -S vim terminus-font
```
编辑locale，找到#en_US.UTF-8 UTF-8和#zh_CN.UTF-8 UTF-8取消注释
``` gradle
vim /etc/locale.gen
```

``` subunit
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
```
生成locale

``` ebnf
locale-gen
```
设置locale

``` bash
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```
## 3.网络配置
设置主机名

``` bash
echo "tanglx-arch" > /etc/hostname
```
安装网络管理器
``` ebnf
pacman -S networkmanager
```
设置开机自启动网络管理器
``` routeros
systemctl enable NetworkManager.service
```
## 4.设置root密码

``` ebnf
passwd
```
## 5.微码
*查看您的 CPU 型号。*

``` gradle
cat /proc/cpuinfo | grep "model name"
```

如果是 Intel CPU，安装 intel-ucode。

``` ebnf
 pacman -S intel-ucode
```

如果是 AMD CPU，安装 amd-ucode。

``` ebnf
 pacman -S amd-ucode
```
## 6.安装引导加载程序

``` ebnf
pacman -S grub efibootmgr
```
安装grub到计算机

``` routeros
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```

如果输出Installation finished. No error reported.表示成功

最后生成 GRUB 配置，即可

``` gradle
grub-mkconfig -o /boot/grub/grub.cfg
```

## 7.重启
退出chroot

``` awk
exit
```

取消挂载

``` gradle
swapoff /dev/sda2 
umount /dev/sda1
umount /dev/sda3
```

