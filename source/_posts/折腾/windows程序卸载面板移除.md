---
title: windows程序卸载面板移除
date: 2024-04-16 09:39:18
categories: 
- 折腾
tags: 
- windows
- 折腾
top: 
---
Windows安装程序后能从控制面板中的卸载找到卸载入口，其实就是通过注册表写入对应键

``` moonscript
计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
```
安装面板的程序卸载键都在注册表下的Uninstall里面

> 可以利用删除注册表键实现
> 1.公司安装软件监控系统，逃避检测
