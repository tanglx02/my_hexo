---
title: debian利用docker部署安全系统
date: 2024-07-28 15:01:17
categories: 
- linux
tags: 
- linux
- debian
- 安全系统
top: 
---
环境
`debian12.6`

## 一、安装与配置docker
1.安装docker
国内安装脚本

``` shell
sudo curl -fsSL https://gitee.com/tech-shrimp/docker_installer/releases/download/latest/linux.sh| bash -s docker --mirror Aliyun
```
2.配置docker镜像地址`sudo vi /etc/docker/daemon.json`

``` json
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io",
        "https://docker.1panel.live",
        "https://hub.rat.dev"
    ]
}
```

重启docker并设置开机自启
`sudo systemctl enable docker`
`sudo systemctl enable docker`
3.安装docker web面板(portainer)

``` javascript
docker run -d --restart=always --name="portainer" -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock registry.cn-beijing.aliyuncs.com/deanmr/portainer-ce:zh-cn
```
## 二、安装mysql

1.拉取镜像
`docker pull mysql`

2.运行镜像

``` javascript
docker run --name mysql --restart=always --privileged=true \
-v /usr/local/mysql/data:/var/lib/mysql \
-v /usr/local/mysql/conf.d:/etc/mysql/conf.d \
-v /etc/localtime:/etc/localtime:ro \
-e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql:latest
```

密码为123456
3.配置mysql

``` javascript
cd /usr/local/mysql
ll
cd conf
vi my.cnf
```
在my.cnf中写入

``` javascript
[client]

default-character-set=utf8mb4

[mysql]

default-character-set=utf8mb4

[mysqld]

# 设置东八区时区
default-time_zone = '+8:00'

# 设置密码验证规则，default_authentication_plugin参数已被废弃

# 改为authentication_policy

#default_authentication_plugin=mysql_native_password
authentication_policy=mysql_native_password

# 限制导入和导出的数据目录
# 为空，不限制导入到处的数据目录；
# 指定目录，必须从该目录导入到处，且MySQL不会自动创建该目录；
# 为NULL，禁止导入与导出功能
#secure_file_priv=/var/lib/mysql
secure_file_priv=

init_connect='SET collation_connection = utf8mb4_0900_ai_ci'

init_connect='SET NAMES utf8mb4'

character-set-server=utf8mb4

collation-server=utf8mb4_0900_ai_ci

skip-character-set-client-handshake

skip-name-resolve
```

4.配置授权远程访问
**进入容器**

``` bash
docker exec -it mysql /bin/bash
```
**登录mysql**

``` javascript
mysql -u root -p
```
**选择数据库**

``` nginx
show databases;
use mysql;
```

 **查看用户连接情况**

``` pgsql
 select host, user, plugin,  authentication_string, password_expired from user;
```

**修改密码认证方式**

``` javascript
ALTER USER root@'%' IDENTIFIED WITH mysql_native_password BY '123456';

ALTER USER root@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';

-- 刷新权限
FLUSH PRIVILEGES;
```

**退出容器**
`exit`

5.重启mysql
设置docker启动时启动mysql

``` javascript
docker update mysql --restart=always
```
重启mysql

``` maxima
docker restart mysql
```