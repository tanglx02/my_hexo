---
title: manjaro i3WM配置
categories:
  - Linux
  - 折腾
tags:
  - Linux
  - 折腾
  - manjaro
abbrlink: 774d72e6
date: 2021-05-31 10:25:00
top:
---

## 安装i3以及其它依赖
i3 整个包组
terminator 终端
dmenu 程序启动器
feh 图片浏览器，展示壁纸
thunar 文件管理
xfce4-appfinder	应用搜索工具
xcompmgr 终端透明
## 快捷键
$mod+Enter 打开默认终端
$mod+shift+e 注销
$mod+shift+q 退出应用
$mod+shift+r 刷新配置

$mod+d    程序搜索
Alt+space 程序菜单
## 修改键位
这里只是针对我的thinkpad x61 笔记本

``` stylus
xmodmap -pke > ~/.xmodmap   //把笔记本键位导入到一个文件中

```

``` ebnf
xev
```

查看键位，按哪个建即可查看它对应的keycode
以下是我的Thinkpad x61 keycode值
左边按键
Esc 9
Caps Lock 66
Ctrl 37
Alt 64
Fn 151
Win 133

交换按键
Esc = Caps Lock 
Caps lock = Esc
fn = ctrl
Ctrl = fn

keycode   66 = Escape NoSymbol Escape
keycode  9 = Caps_Lock NoSymbol Caps_Lock
keycode 37 = XF86WakeUp NoSymbol XF86WakeUp
keycode  151 = Control_L NoSymbol Control_L


## 配置
* 配置字体大小

``` stylus
vim .Xresources 
Xft.dpi:200
```

