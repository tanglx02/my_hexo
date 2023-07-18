---
title: manjaro录音降噪
date: 2023-07-18 14:37:46
categories:
- Linux
tags:
- Linux
- manjaro
- 降噪
top: 
---
# 前言
录视频时候发现有噪音问题，网上找了很久，没有找到办法，archwiki有相关教程也没能解决，于是想到以前kalilinux作为主力机时候也有出现过这个问题，于是用相同的方法解决了这个问题。
# 操作步骤

**1.备份配置文件**

``` shell
sudo cp /etc/pulse/default.pa /etc/pulse/default.pa.bak 
```
2.修改配置文件

``` shell
sudo vim /etc/pulse/default.pa 
```

3.将下面的代码添加到default.pa文件结尾

``` shell
#Active Noise Removal
.ifexists module-echo-cancel.so
load-module module-echo-cancel aec_method=webrtc source_name=mic source_properties=device.description=MicHD
set-default-source "mic"
.endif 
```

> 此方法测试发现能够使用在debian发行版和arch发行版，其它linux自测