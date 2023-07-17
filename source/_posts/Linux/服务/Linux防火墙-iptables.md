---
title: Linux防火墙-iptables
categories:
  - Linux
  - 服务
tags:
  - Linux
  - 服务
  - 防火墙
abbrlink: 32a8c543
date: 2021-04-27 15:07:22
top:
---
## 策略与规则链
防火墙会从上至下的顺序来读取配置的策略规则，在找到匹配项后就立即结束匹配工作并去执行匹配项中定义的行为（即放行或阻止）。如果在读取完所有的策略规则之后没有匹配项，就去执行默认的策略。一般而言，防火墙策略规则的设置有两种：一种是“通”（即放行），一种是“堵”（即阻止）。当防火墙的默认策略为拒绝时（堵），就要设置允许规则（通），否则谁都进不来；如果防火墙的默认策略为允许时，就要设置拒绝规则，否则谁都能进来，防火墙也就失去了防范的作用。
## 参数

| 参数 | 作用 |
| --- | --- |
| -P | 设置默认策略 |
| -F | 清空规则链 |
| -L | 查看规则链 |
| -A | 在规则链的末尾加入新规则 |
| -I  | 在规则链的头部加入新规则 |
| -D  | 删除某一条规则 |
| -s[!] | 匹配来源地址IP/MASK，加叹号“!”表示除这个IP外 |
| -d[!] | 匹配目标地址 |
| -i 网卡名称 | 封包所进入的那个网络接口，例如 eth0, lo 等接口。需与 INPUT 链配合 |
| -o 网卡名称 | 封包所传出的那个网络接口，需与 OUTPUT 链配合 |
| -p[!]| 匹配协议，主要的封包格式有： tcp, udp, icmp 及 all|
| --sport[!]  | 匹配来源端口号 |
| --dport[!] | 匹配目标端口号 |
|-j|后面接动作，主要的动作有接受(ACCEPT)、丢弃(DROP)、拒绝(REJECT)及记录(LOG)|
==加！代表除此之外 #F44336==
格式

``` inform7
[root@www ~]# iptables [-PFLAI 链名] [-io 网络接口] [-s 来源IP/网域] [-d 目标IP/网域] [-p 协议] [-dport 目标端口] [-sport 来源端口] [ -j ACCEPT|DROP|REJECT|LOG]
```
==链名 #F44336==-接口--网域-协议-端口-==规则 #F44336==

## 四表五链

四表:filter,nat,mangle,raw，默认表是filter（没有指定表的时候就是filter表）。表的处理优先级：raw>mangle>nat>filter。

          filter：一般的过滤功能

          nat:用于nat功能（端口映射，地址映射等）

          mangle:用于对特定数据包的修改

          raw:有限级最高，设置raw时一般是为了不再让iptables做数据包的链接跟踪处理，提高性能

     RAW 表只使用在PREROUTING链和OUTPUT链上,因为优先级最高，从而可以对收到的数据包在连接跟踪前进行处理。一但用户使用了RAW表,在某个链 上,RAW表处理完后,将跳过NAT表和 ip_conntrack处理,即不再做地址转换和数据包的链接跟踪处理了.

         RAW表可以应用在那些不需要做nat的情况下，以提高性能。如大量访问的web服务器，可以让80端口不再让iptables做数据包的链接跟踪处理，以提高用户的访问速度。
五链：PREROUTING,INPUT,FORWARD,OUTPUT,POSTROUTING。

           PREROUTING:数据包进入路由表之前

           INPUT:通过路由表后目的地为本机

           FORWARD:通过路由表后，目的地不为本机

           OUTPUT:由本机产生，向外转发

           POSTROUTIONG:发送到网卡接口之前
	

## 四规则
ACCEPT 
允许
DROP
拒绝
REJECT
拒绝且回复
LOG
记录到系统日志，/var/log/messages
## iptables-save
备份

``` elixir
root@localhost ~]# iptables-save >/var/bak/iptables/iptables.bak  
```

恢复


    [root@localhost ~]# iptables-restore </var/bak/iptables/iptables.bak    
修改

## 相关文章
[博客园](https://www.cnblogs.com/paul8339/p/6515410.html)
[Linux就该这么学](https://www.linuxprobe.com/chapter-08.html)

