---
title: manjaro其它的配置
categories:
  - Linux
  - 折腾
tags:
  - Linux
  - 折腾
  - manjaro
abbrlink: 8d91099f
date: 2021-05-31 10:27:00
top:
---

## 修改家目录为英文
1.修改家目录环境变量

``` javascript
vim ~/.config/user-dirs.dirs
```
修改为以下内容
``` makefile
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOWNLOAD_DIR="$HOME/Download"
XDG_TEMPLATES_DIR="$HOME/Templates"
XDG_PUBLICSHARE_DIR="$HOME/Public"
XDG_DOCUMENTS_DIR="$HOME/Documents"
XDG_MUSIC_DIR="$HOME/Music"
XDG_PICTURES_DIR="$HOME/Pictures"
XDG_VIDEOS_DIR="$HOME/Videos"
```
2.修改家目录中的中文名

``` cos
cd ~
mv 公共 Public
mv 模板 Templates
mv 视频 Videos
mv 图片 Pictures
mv 文档 Documents
mv 下载 Download
mv 音乐 Music
mv 桌面 Desktop
```
## 配置v2ray
![](https://storage-cn.github.io/images/2021/20210603124748.png)
一、v2ray安装

``` nginx
yay -S v2raya
```

二、v2ray-core安装

``` vim
yay -S xray
```
三、启动v2ray

``` smali
sudo systemctl start v2raya #启动
sudo systemctl stop v2raya  # 关闭
sudo systemctl enable v2raya #开机自启动
sudo systemctl disable v2raya #开机不启动


```

