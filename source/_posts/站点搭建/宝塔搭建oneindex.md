---
title: 宝塔搭建Oneindex
categories:
  - 站点搭建
tags:
  - oneindex
  - 图传
  - 存储
  - 云盘
  - onedrive
abbrlink: aeef8a84
date: 2020-11-10 15:48:25
top:
---

## 一、基本介绍

![](https://storage.freecplus.top/images/2020/11/10/20201110155125.png)
   OneIndex针对Onedrive网盘的一个开源程序。可以将Onedrive存储的文件展示，直连下载。视频还能在线播放！不用服务器空间，不走服务器流量！
不建议用来做 床图，oneindex虽然上传下载不需要走自己的服务器，不过还是需要有服务器的辅助，不易做床图的之类的关键节点。
### 效果图
![](https://storage.freecplus.top/images/2020/11/10/20201110155953.png)
![](https://storage.freecplus.top/images/2020/11/10/20201110160116.png)
![](https://storage.freecplus.top/images/2020/11/10/20201110160153.png)
## 二、准备工作
服务器一台，域名，准备一个OneDrive账号
php5.6、Nginx、Redis
以及下载[oneindex](https://pan.baidu.com/s/1GP_oB_k_9Dq2fCYaAepo8g)，提取码:4vxs
## 三、宝塔配置
1、安装Redis![](https://storage.freecplus.top/images/2020/11/10/20201110161510.png)
2、php5.6以及php中的扩展REdis
![](https://storage.freecplus.top/images/2020/11/10/20201110161628.png)
3、绑定并选择php5.6，不需要数据库
![](https://storage.freecplus.top/images/2020/11/10/20201110161811.png)
4、配置ssl证书，并设置伪静态
![](https://storage.freecplus.top/images/2020/11/10/20201110162017.png)
![](https://storage.freecplus.top/images/2020/11/10/20201110162149.png)
伪静态

``` nginx
if (!-f $request_filename){
    set $rule_0 1$rule_0;
}
if (!-d $request_filename){
    set $rule_0 2$rule_0;
}
if ($rule_0 = "21"){
    rewrite ^/(.*) /index.php?/$1 last;
}
```
5、oneindex解压至安装路径
![](https://storage.freecplus.top/images/2020/11/10/20201110162505.png)
修改cenoroller目录下的Admincontroller.php,框中部分改成自己的域名
![](https://storage.freecplus.top/images/2020/11/10/20201110162742.png)
## 四、登录 azure 获得机密与ID
1、访问自己的域名
![](https://storage.freecplus.top/images/2020/11/10/20201110163606.png)
2、点击获取机密和id这里需要记得依次保存
![](https://storage.freecplus.top/images/2020/11/10/20201110163632.png)
![](https://storage.freecplus.top/images/2020/11/10/20201110163045.png)
![](https://storage.freecplus.top/images/2020/11/10/20201110163632.png)
最后这个是id
![](https://storage.freecplus.top/images/2020/11/10/20201110163922.png)

## 五、安装
1、输入刚刚的密码和id
2、然后就是说绑定你的onedrive账号![](https://storage.freecplus.top/images/2020/11/10/20201110164016.png)
3、绑定成功
![](https://storage.freecplus.top/images/2020/11/10/20201110164127.png)

## 六、完善
安装完成后有很多玩法，看自己需求这里我就做一下基本都要做的
1、修改网站显示路径
默认都是显示\目录下的所有文件我一般不喜欢这么做
![](https://storage.freecplus.top/images/2020/11/10/20201110164528.png)
2、上传文件后台是可以上传的，不过那样比较繁琐，它只能从服务器上传上去到onedrive，我一般是本地安装一个onedrive软件，直接上传上去到我的/storage目录
3、文件上传上去是不会立即在网站上显示的，你需要点击“重构所有缓存”，当然我猜没有人想每次都来后台点击，所以你可以复制shell脚本在宝塔的“计划任务中来自动执行”
脚本
![](https://storage.freecplus.top/images/2020/11/10/20201110165221.png)

手动
![](https://storage.freecplus.top/images/2020/11/10/20201110164931.png)
自动
![](https://storage.freecplus.top/images/2020/11/10/20201110165301.png)