---
title: docker基本使用
date: 2024-11-20 16:22:35
categories: 
- 工具
tags: 
- 工具
- docker
top: 
---
# 一、docker安装
**1.官网方式安装**
**2.docker网页管理工具**
*docker正确安装后使用命令安装*
安装中文版 2.19.5 
``` javascript
 docker run -d --restart=always --name="portainer" -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock 6053537/portainer-ce
```
安装中文版2.11.0 

``` javascript
 docker run -d --restart=always --name="portainer" -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock newrain857/portainer-ce-cn
```

# 二、常用命令
[详细博客](https://blog.csdn.net/qq_44700578/article/details/136456291)
## 1.基础命令

``` shell
systemctl start docker           #启动docker
systemctl stop docker            #关闭docker
systemctl restart docker         #重启docker
systemctl enable docker          #设置开机自启动
systemctl status docker          #查看docker运行状态
systemctl status docker.service     #查询Docker服务状态
docker version                   #查看docker版本号信息
docker info                      #查看docker相关信息，包括版本信息、镜像和容器数量等
docker stats                     #检查docker守护进程是否在运行
docker --help                    #docker命令提示
```

## 2.docker镜像命令

``` shell
docker images  #查看镜像

#从Docker Hub查找/搜索镜像
docker search [options] TERM      
docker search -f STARS=9000 mysql  #搜索stars收藏数不小于10以上的mysql镜像

#从服务器拉取镜像拉取镜像
docker pull 镜像名       #拉取最新版本的镜像
docker pull 镜像名:tag   #拉取镜像，指定版本
#推送镜像到服务
docker push 镜像名
docker push 镜像名:tag


docker save -o 保存的目标文件名称 镜像名 #保存镜像为一个压缩包
docker load -i 文件名    #加载压缩包为镜像


#删除镜像。当前镜像没有被任何容器使用 才可以删除
docker rmi 镜像名/镜像ID     #删除镜像 
docker rmi -f 镜像名/镜像ID  #强制删除
docker rmi -f 镜像名 镜像名 镜像名     #删除多个 其镜像ID或镜像用用空格隔开即可 
docker rmi -f $(docker images -aq)  #删除全部镜像，-a 意思为显示全部, -q 意思为只显示ID

docker image rm 镜像名称/镜像ID  #强制删除镜像


#给镜像打标签【有时候根据业务需求 需要对一个镜像进行分类或版本迭代操作，此时就需要给镜像打上标签】
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

```
## 3.docker容器命令
 

``` shell
docker ps      #显示正在运行的容器
docker ps -a   #-a,--all  显示全部容器，包括已停止的（默认只显示运行中的容器）

#容器怎么来？ docker run 创建并运行一个容器，处于运行状态。
#--name 给要运行的容器起的名字；   -p 将宿主机端口与容器端口映射，冒号左侧是宿主机端口，右侧是容器端口；   -d 表示可后台运行容器 （守护式运行）。具体样例见下
docker run --name containerName -p 80:80 -d nginx  

docker pause 容器名/容器ID    #让一个运行的容器暂停
docker unpause name  #让一个容器从暂停状态恢复运行
docker stop name     #停止一个或多个运行的容器（杀死进程、回收内存，仅剩文件系统）
docker start name    #让一个停止的容器再次运行
docker start mysql redis rabbitmq nginx   #启动多个容器
docker restart name  #重启一个或多个容器
#docker stop与docker kill的区别：都可以终止运行中的docker容器。类似于linux中的kill和kill -9这两个命令，docker stop与kill相似，docker kill与kill -9类似
docker kill 容器名    #杀掉一个或多个运行中的容器
docker rename 容器名 新容器名  #更换容器名

#删除容器
docker rm 容器名/容器ID            #删除容器  
docker rm -f CONTAINER           #强制删除
docker rm -f 容器名 容器名 容器名   #删除多个容器 空格隔开要删除的容器名或容器ID
docker rm -f $(docker ps -aq)    #删除全部容器


docker inspect 容器名         #获取容器更多信息 
docker ps -l                 #最后一次运行的容器
docker port 容器名/容器ID     #查看端口的映射情况
docker logs 容器名           #查看容器运行日志         
docker logs -f 容器名        #持续跟踪日志
docker logs -f --tail=20 容器名  #查看末尾多少行
docker diff 容器名        #查看容器的改动



#进入容器执行命令，两种方式 docker exec 和 docker attach，推荐docker exec
#方式一 docker exec。
docker exec -it 容器名/容器ID bash
#方式二 docker attach，推荐使用docker exec
docker attach 容器名/容器ID

#从容器退到自己服务器中（不能用ctrl+C）
exit      #直接退出。未添加-d(持久化运行容器)时，执行此参数 容器会被关闭
ctrl+p+q  #优雅退出。无论是否添加-d参数，执行此命令容器都不会被关闭

```