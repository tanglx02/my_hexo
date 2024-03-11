---
title: 华为设备开启dhcp服务
date: 2024-03-11 16:27:46
categories: 
- 网络
tags: 
- 网络
- 华为
- 命令
- dhcp
- 数通
top: 
---
# 华为设备开启dhcp服务

![enter description here](https://picture.tanglx.cn/web/2024/1710146368786.png)
**1.对AR1路由器进行配置**
``` routeros?linenums
<AR1>system-view 	//进入系统视图
[AR1]int GigabitEthernet 0/0/0	//进入接口
[AR1-GigabitEthernet0/0/0]ip add 192.168.1.1 255.255.255.0   //配置接口ip
[AR1-GigabitEthernet0/0/0]quit	//退到系统视图
[AR1]dhcp enable		//开启dhcp服务
[AR1]int g0/0/0			进入接口
[AR1-GigabitEthernet0/0/0]dhcp select interface   //指定接口开启dhcp
```



**之后局域网下pc就能获取到ip地址**
![enter description here](https://picture.tanglx.cn/web/2024/1710146299692.png)