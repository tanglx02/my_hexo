---
title: pacman包管理器
date: 2024-04-25 00:01:00
categories: 
- linux
tags: 
- archlinux
- 包管理器
top: 
---
[toc]
# 一、pacman包管理器用法

<table data-draft-node="block" data-draft-type="table" data-size="normal" data-row-style="normal"><tbody><tr><th>功能</th><th>命令</th></tr><tr><td>安装软件包（组）</td><td># pacman -S 软件包（组）名</td></tr><tr><td>移除软件包</td><td># pacman -R 软件包名</td></tr><tr><td>移除软件包及其未被其他软件包要求的依赖</td><td># pacman -Rs 软件包名</td></tr><tr><td>同步软件数据库并更新系统</td><td># pacman -Syu</td></tr><tr><td>查询软件数据库</td><td>$ pacman -Ss 字符串</td></tr><tr><td>查询文件</td><td># pacman -F 字符串</td></tr></tbody></table>

## 1、软件包缓存清理
使用 pacman 安装和更新软件包时，软件包会下载到 /var/cache/pacman/pkg/ 目录下。久而久之，缓存会占据大量的存储空间。因此，定期清理软件包缓存是必要的。

请安装 pacman-contrib 软件包，然后开机自动启动 paccache.timer，以便每周自动清理不使用的软件包缓存。

``` shell
# pacman -S pacman-contrib
# systemctl enable paccache.timer
```

## 2、pacman 的使用注意事项
软件包管理是系统维护的一部分。作为管理员，使用计算机的时候一定要负起系统管理员的责任。如果您热爱 Linux 的开放与可定制性，就要有能力遵守 Linux 的维护规则，以免破坏系统。

使用 pacman 的注意事项如下：

- 更新系统前作好准备
- 禁止部分更新
- 注意更新时的提醒
- 定期检查孤立包

### 2.1更新系统前作好准备
我们已经知道，在 Arch Linux 中，系统更新的命令是 pacman -Syu。绝大多数情况下，pacman 可以帮您处理好一切事务，但也有例外。当系统更新无法自动完成，需要用户手动干预时，Arch Linux 主页会定期发布新闻，提供系统更新指南。

笔者建议您在系统更新之前，前往 Arch Linux 主页 查看最新消息。如果更新需要不寻常的用户操作介入时（无法简单地按照 pacman 的输出信息处理），以上信息总会给出合适的方法。

此外，有时重要软件包更新时，会引发一些严重的问题，俗称“滚炸了”。查看 Arch Linux 相关论坛和群组，有助于避免这些问题。笔者推荐的论坛和群组如下：

<ul><li data-pid="OwUakM3t"><a href="https://link.zhihu.com/?target=https%3A//bbs.archlinux.org/" class=" wrap external" target="_blank" rel="nofollow noreferrer" data-za-detail-view-id="1043">Arch Linux 论坛</a></li><li data-pid="Gg4dXLEa"><a href="https://link.zhihu.com/?target=https%3A//bbs.archlinuxcn.org/" class=" wrap external" target="_blank" rel="nofollow noreferrer" data-za-detail-view-id="1043">Arch Linux 中文论坛</a></li><li data-pid="4Yilo-BB"><a href="https://link.zhihu.com/?target=https%3A//www.archlinuxcn.org/archlinuxcn-group-mailling-list/" class=" wrap external" target="_blank" rel="nofollow noreferrer" data-za-detail-view-id="1043">Arch Linux 中文社区交流群</a></li></ul>
最后，系统更新出现问题是难以避免的。因此，请不要在重要任务前进行系统更新，而是留出足够的时间用于应付可能的问题。

### 2.2禁止部分更新
`pacman -Sy` 命令用于下载软件包数据库，但不更新系统中的软件包。这种操作就称为“部分更新”。部分更新是危险的。当您下载软件包数据库（`pacman -Sy`）之后，如果安装新软件（`pacman -S`），可能造成依赖关系被破坏。

很简单，请记住一点：

不要使用 `pacman -Sy`，而是使用 `pacman -Syu`。
### 2.3注意更新时的提醒
当升级系统时， 请一定要注意 pacman 输出的注意信息。 如果有需要用户手动操作的，请一定要立即搞定。 如果不明白 pacman 输出的信息， 请去论坛搜索或者看 Arch Linux 首页的新闻。

当配置文件发生更新，或者卸载软件包的时候，pacman 可能会生成 pacnew 和 pacsave 文件。这些文件可以用 pacdiff 处理。

``` shell
# pacdiff  # 处理 pacnew 和 pacsave 文件
```

### 2.4定期检查孤立包
更新系统后，有些软件包不再作为依赖，或者不再属于官方仓库。您可以定期用以下命令清除或查看它们

``` shell
# pacman -Qtdq | pacman -Rns -  # 递归删除孤立软件包及其配置文件
$ pacman -Qqd | pacman -Rsu --print -  # 查看循环依赖、额外依赖
$ pacman -Qm  # 查看不属于远程仓库的软件包，请注意下面要介绍的 AUR 软件包也包括在其中
```
## 3.软件仓库镜像
软件仓库镜像（镜像源）是软件仓库的复制品，部署在全球各地，以便于用户获取软件包。我们在安装过程中已经选择了合适的镜像源，但是为了保证镜像源的可用性，需要定期重新设置镜像源。

### 3.1官方镜像源列表
欲查看官方镜像源列表，请查看 [这里](https://archlinux.org/mirrors/status/)。笔者十分建议您选择“同步成功的镜像源（Successfully Syncing Mirrors）”。

### 3.2手动设置镜像源
编辑 /etc/pacman.d/mirrorlist 以便手动设置镜像源，将您要使用的镜像源放在“Server =”后面即可。

``` asciidoc
$ sudo -e /etc/pacman.d/mirrorlist

/etc/pacman.d/mirrorlist
------------------------
Server = https://geo.mirror.pkgbuild.com/$repo/os/$arch
```

设置镜像源之后，使用以下命令刷新本地软件包列表。

``` shell
# pacman -Syyu  # 使用两个“y”，强制刷新软件包列表
```

