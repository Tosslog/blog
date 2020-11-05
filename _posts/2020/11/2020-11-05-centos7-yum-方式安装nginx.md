---
layout:     post 
title:      "centos7 yum 方式安装nginx"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - centos
    - yum
    - nginx
---

> centos7系统库中默认是没有nginx的rpm包的，所以我们自己需要先更新下rpm依赖库
## 1、使用yum安装nginx需要包括Nginx的库，安装Nginx的库
```shell
# rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```
## 2、使用下面命令安装nginx
``` shell
shell# yum install nginx
```
## 3、启动Nginx
``` shell
shell# service nginx start
或
shell# systemctl start nginx.service
```
