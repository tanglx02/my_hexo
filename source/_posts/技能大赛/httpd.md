---
title: httpd
categories:
  - 技能大赛
tags:
  - 技能大赛
abbrlink: bd25e061
date: 2021-05-09 23:09:36
top:
---

## 

## 加端口

如果要使用除443和80 端口外需要在全局模式里加入listen *

`Listen 8080` //例如8080

## 虚拟目录

`:553`行，或者`/Alias`

 `Alias /test "/yum"`     //定义虚拟目录“/test”，物理路径为“/yum”！

## 密码认证

1.`/Alias`后找到下面部分，复制到要加密的虚拟机下面

`<Directory "/var/www/icons">`
    `Options Indexes MultiViews FollowSymLinks`
    `AllowOverride None`
    `Order allow,deny`
    `Allow from all`
`</Directory>`

2.修改为

`<Directory "/var/www/icons">`
    `Options Indexes MultiViews FollowSymLinks`
    `AllowOverride authconfig`   //这部分
    `Order allow,deny`
    `Allow from all`
`</Directory>`

3. 创建密码文本(passwd 是输出的文本)

   `[root@localhost conf]# htpasswd -c passwd tonlx` //第一次加-c

   `[root@localhost conf]# htpasswd  passwd tonlx2`  

   4.

## ssl

