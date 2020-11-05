---
layout:     post 
title:      "配置centos7解决 docker Failed to get D-Bus connection 报错"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - centos
    - docker
---
> ***博客使用的 github pages 对于大陆访问不太友好，如遇到内容缺失或是无法显示图片等问题，请科学访问！***

## 方法一

当你运行 systemctl start xxxx 的时候发现提示 docker Failed to get D-Bus connection

- 原因及解决方式： 

这个的原因是因为dbus-daemon没能启动。其实systemctl并不是不可以使用。将你的CMD或者entrypoint设置为/usr/sbin/init即可。会自动将dbus等服务启动起来。 
然后就可以使用systemctl了。命令如下：

``` shell
# 在创建docker容器时添加--privileged 其余的根据需要修改  如container=docker 与 centos 字段
docker run --privileged  -ti -e "container=docker"  -v /sys/fs/cgroup:/sys/fs/cgroup  centos  /usr/sbin/init
```
如果是群晖下的docker，先进入到群晖ssh 在输入上面的命令

## 方法二
报错信息：
Failed to get D-Bus connection: Operation not permitted
处理办法：
启动docker时，使用privileged 参数
``` shell
docker run --privileged -i -t  -p 10080:80 centos /usr/sbin/init
```
启动时间非常长，可以另开一个窗口docker ps -a 获得containerid，然后
``` shell
docker stop containerid 
或者
docker start containerid
```
连接docker使用
``` shell
#群辉使用方法：
docker exec -it 容器名称  /bin/bash
如果出现：
Error response from daemon: Container xxxxxxxxxx is not running
#说明没有运行 容器 或者说生面的 docker run 运行失败 
```
如果是群晖下的docker，先进入到群晖ssh 在输入上面的命令
