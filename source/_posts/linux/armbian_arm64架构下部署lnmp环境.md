---
title: armbian_arm64架构下部署lnmp环境
date: 2024-03-18 18:44:55
categories: 
- linux
tags: 
- linux
- armbian
- arm64
- lnmp
top: 
---
[toc]
# 一、基本设置
**1.更新软件源**

``` bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

**2.关闭防火墙**

``` bash
 vim /etc/ufw/ufw.conf 	//编辑配置文件
ENABLED=no			//将内容从yes值改为no
```

# 二、mysql安装与配置
**1.安装mysql**

``` bash
sudo apt-get install mysql-server
```

**2.启动mysql**

``` bash
sudo systemctl start mysql 
sudo systemctl enable mysql
```
**3.修改mysql密码**
``` bash
mysql -u root -p	//登录mysql默认密码为空，直接回车
use mysql;
CREATE USER 'root'@'%' IDENTIFIED BY 'new_password';  // 创建局域网络账号
GRANT ALL ON *.* TO 'root'@'%' WITH GRANT OPTION; // 分配权限
ALTER USER 'root'@'%' IDENTIFIED BY 'new_password';	//new_password为新密码
alter user 'root'@'%' identified with mysql_native_password by 'new_password';  //远程密码
FLUSH PRIVILEGES;	//刷新权限使更改生效
EXIT;		//退出mysql
```
**4.mysql修改配置文件开启远程**

``` gradle
vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
修改配置文件，注释掉bind-address = 127.0.0.1  和 mysqlx-bind-address    = 127.0.0.1

4.重启mysql

``` maxima
systemctl restart mysql
```


# 三、php的安装
**1.安装PHP及所需模块**
``` bash
sudo apt-get install php-fpm php-mysql php-common php-mbstring php-xml php-cli php-gd php-curl
sudo systemctl start php8.1-fpm    //可能和我版本不一样，自查后修改
sudo systemctl enable php8.1-fpm	//可能和我版本不一样，自查后修改
```


# 四、nginx安装与配置
**1.安装nginx并设置开机自启动**

``` bash
sudo apt-get install nginx
systemctl start nginx.service 
systemctl enable nginx.service 
```
**2.配置Nginx与PHP处理：**
 
 1)编辑配置文件

``` bash
sudo vim /etc/nginx/sites-available/default
```
2)在文件中添加以下内容以处理PHP请求：(1.注意需要将内容包含到server{}中2.php*.*版本根据自身安装版本选择)
``` bash
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
}
```
3)之后将index.php 添加到server{}中，将默认识别改文件
 

``` delphi
index index.php index.html index.htm;
```

4)测试并重启nginx服务
sudo nginx -t
sudo systemctl restart nginx

)其它需要参考模板修改

``` bash
server {
    listen 80;	
    server_name example.com;
    root /var/www/html;
 
    index index.php index.html index.htm;
    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
 
    location / {
        try_files $uri $uri/ =404;
    }
 
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock; # 根据PHP版本和配置调整
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```