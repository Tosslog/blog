---
layout:     post 
title:      "Centos 7 安装 netdata"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - centos
    - netdata
---
> ***博客使用的 github pages 对于大陆访问不太友好，如遇到内容缺失或是无法显示图片等问题，请科学访问！***


1. 如果还没安装git就先安装下git
```shell
$ sudo yum -y install git
```
2. 安装好 git 后，你要把仓库 “clone” 到你的系统里。运行下面的命令。

> 这个命令会在当前工作目录克隆（或者说复制一份）仓库

```shell
$ git clone https: //github.com/firehol/netdata.git
```
3. 先安装一些依赖包
```shell
$ yum -y install zlib-devel libuuid-devel libmnl-devel gcc make git autoconf autogen automake pkgconfig
```
> 当所有需要的软件包都安装好了，你就 cd 到 netdata/ 目录，运行 netdata-installer.sh 脚本。

```shell
$ sudo ./netdata-installer.sh
```
4. 运行/停止

```shell
/opt/netdata/sbin/netdata
```

```shell
--- starting netdata --- 
--- Start netdata ---
[/opt/netdata]# stop_all_netdata 
OK
[/opt/netdata]# /opt/netdata/bin/netdata 
OK 
```

5. 杀死进程
```shell
killall netdata
```

