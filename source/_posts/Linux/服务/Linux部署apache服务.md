---
title: Linux部署apache服务
categories:
  - Linux
  - 服务
tags:
  - Linux
  - 服务
  - apache
  - httpd
abbrlink: d9ea19c9
date: 2021-04-30 11:06:42
top:
---

# Linux部署apache服务
## 安装

``` ebnf
yum install httpd
```
设置开机自启与启动

``` livecodeserver
service httpd start
chkconfig httpd on
```

## 配置文件

| 作用 | 文件名称 |
| --- | --- |
| 服务目录 | /etc/httpd |
| 主配置文件 | /etc/httpd/conf/httpd.conf |
| 网站数据目录 | /var/www/html |
| 访问日志 | /var/log/httpd/access_log   [common] [combined] |
| 错误日志 | /var/log/httpd/error_log |

## 配置参数

| ServerRoot | 服务目录 |
| --- | --- |
| ServerAdmin | 管理员邮箱 |
| User | 运行服务的用户 |
| Group | 运行服务的用户组 |
| ServerName | 网站服务器的域名 |
| DocumentRoot | 网站数据目录|
| Listen| 监听的IP地址与端口号 |
| DirectoryIndex | 默认的索引页页面 |
| ErrorLog | 错误日志文件 |
| CustomLog | 访问日志文件 |
| Timeout | 网页超时时间,默认为300秒 |
| Include | 需要加载的其他文件 |

## 设置登录验证