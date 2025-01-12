title: debian基础配置
date: 2024-07-28 13:53:26
categories:

* linux
  tags:

* linux

* debian
  top:

# 一、配置软件源

编辑`/etc/apt/sources.list`，添加下面地址(bookworm为debian12的代号，其它debian需要更换代号)

```shell
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware

```

更新源

```shell
sudo apt update
```

# 二、配置静态地址

查看网卡名称`ip a`
编辑网卡配置文件`vi /etc/network/interfaces`

```shell
auto ens32
allow-hotplug ens32
iface ens32 inet static
address 192.168.88.150
netmask 255.255.255.0
gateway 192.168.88.2

```

重启网卡`systemctl restart networking.service`

配置dns`vi /etc/resolv.conf`

```shell
nameserver 114.114.114.114
nameserver 8.8.8.8
nameserver 8.8.8.4

```

