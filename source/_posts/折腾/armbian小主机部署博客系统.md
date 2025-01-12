---
title: armbian小主机部署博客系统
date: 2024-11-20 16:54:36
categories: 
- 折腾
tags: 
- 折腾
- armbian
- 博客
- zblog
top: 
---
[toc]

# 1.安装nginx等环境
nginx相比apache更加轻量节省空间

``` javascript
sudo apt update
sudo apt upgrade
sudo systemctl restart nginx
sudo apt install php-sqlite3
sudo apt install php7.3 php7.3-fpm php7.3-cli
```
配置Nginx与PHP-FPM

``` javascript
vim /etc/nginx/sites-available/default
```
添加

``` javascript
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php7.3-fpm.sock;
}
```
重启nginx与php-fpm

``` javascript
sudo systemctl restart nginx
sudo systemctl restart php7.3-fpm
```

测试安装

``` javascript
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```
在浏览器中访问http://<your_server_ip>/info.php，你应该看到PHP信息页面。如果页面显示了PHP版本，说明安装成功

# 2.安装zblog
[官网](https://www.zblogcn.com/)
本机使用版本为1.7