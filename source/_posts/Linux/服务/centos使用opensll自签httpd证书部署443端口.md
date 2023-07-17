---
title: centos使用opensll自签httpd证书部署443端口
categories:
  - Linux
  - 服务
tags: 'Linux,服务,openssl,apache - Linux - 服务 - openssl - apache'
abbrlink: 99d7f6b5
date: 2021-04-29 20:40:12
top:
---

安装httpd和ssl模块

``` nginx
yum install httpd mod_ssl
```
生成密钥

``` lsl
openssl genrsa -out www.2021skills.com.key 2048
```

生成请求文件csr

``` css
openssl req -new -key www.2021skills.com.key -out www.2021skills.com.csr
```

生成证书

``` stylus
openssl x509 -req -days 365 -in www.2021skills.com.csr -signkey www.2021skills.com.key -out www.2021skills.com.crt
```
部署

``` stylus
cp www.2021skills.com.key /etc/pki/tls/private/
cp www.2021skills.com.crt /etc/pki/tls/certs/
```

修改 /etc/httpd/conf.d/ssl.conf
![](https://storage.freecplus.top/images/2021/20210430100926.png)
修改 /etc/httpd/conf/httpd.conf 
![](https://storage.freecplus.top/images/2021/20210430101048.png)

## 相关文章
