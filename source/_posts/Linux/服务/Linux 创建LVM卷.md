---
title: Linux 创建LVM卷
categories:
  - Linux
  - 服务
tags:
  - Linux
  - 服务
  - LVM
abbrlink: 1cbd8300
date: 2021-04-08 20:04:28
top:
---
LVM(logical volume Manager) 逻辑卷管理，通过将底层物理硬盘抽象封装起来，以逻辑卷的形式表现给上层系统，逻辑卷的大小可以动态调整而且不会丢失现有数据。新加入的硬盘也不会改变现有上层的逻辑卷。

+ PE (physical Extend)

  默认大小4M

+ PV (physical volume) 物理卷

+ VG (volume group)卷组

+ LV (logical volume)逻辑卷



![LVM](https://storage.freecplus.top/images/2020/12/15/20201215110441.png)

### 常用LVM的部署命令

| 功能/命令 | 物理卷管理 | 卷组管理 | 逻辑卷管理 |
| --- | --- | --- | --- |
| 扫描 | pvscan | vgscan | lvscan |
| 建立 | pvcreate | vgcreate | lvcreate |
| 显示 | pvdisplay | vgdisplay | lvdisplay |
| 删除 | pvremove | vgremove | lvremove |
| 扩展 |  | vgextend | lvextend |
| 缩小 |  | vgreduce | lvreduce |

### 1、创建LVM

1.将物理磁盘设备初始化为物理卷

``` q
pvcreate /dev/sdb /dev/sdc
```

2.创建卷组，并将PV加入到卷组中

``` q
vgcreate thin /dev/sdb /dev/sdc
```

3、基于卷组创建逻辑卷

``` lsl
lvcreate -n thin_1 -L 2G thin  // -n 逻辑卷的名称 -L 逻辑卷 thin卷组
```

4、为创建好的逻辑卷创建文件系统

``` stylus
mkfs.ext4 /dev/thin/thin_1
```

5、将格式化好的逻辑卷挂在使用

``` groovy
mount /dev/thin/thin_1 /thin_1
```

### 2、卸载LVM

1.取消LV的挂载

``` nginx
umount /thin_1
```

2.卸载LV

``` nginx
lvremove /dev/thin/thin_1 
```

3.卸载VG

``` ebnf
vgremove thin 
```

4.卸载PV

``` q
pvremove /dev/sdb /dev/sdc
```

<u>卸载需要按顺序进行操作，比如要卸载PV就要从1执行到5，卸载LV就要从1执行到2</u><u>(即，先取消挂载在卸载LV)</u>

### 3、LV逻辑卷的拉伸
**1、保证VG有足够的空间**
vgs
**2、扩展逻辑卷**
比如我要扩展/home 大小，首先确认自己的VG(卷组)空间够不够，如果不够需要先扩展卷组
 2.1 初始化物理卷

``` nginx
 pvcreate /dev/sdc
```

2.2 加入卷组

``` stylus
vgextend centos /dev/sdc
```

2.3 扩展逻辑卷

``` lsl
lvextend /dev/centos/home -L +10G
```

**3、查看扩展后的逻辑卷大小**

``` ebnf
lvs
```

**4、更新文件系统**
如果使用xfs文件系统

``` nginx
 xfs_growfs /dev/centos/home
```
 如果使用ext4文件系统

``` nginx
    resize2fs /dev/centos/home
```

