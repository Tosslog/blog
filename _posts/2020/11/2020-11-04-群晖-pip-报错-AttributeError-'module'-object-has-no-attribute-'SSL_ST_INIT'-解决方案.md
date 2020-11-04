---
layout:     post 
title:      "群晖 pip 报错 AttributeError 'module' object has no attribute 'SSL_ST_INIT' 解决方案"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - 群晖
    - synology
    - pip
---

## 呈现的错误 
> AttributeError 'module' object has no attribute 'SSL_ST_INIT'


![img](../img/post-img/2020/11/04/1171771448.jpg)

## 解决方案

### 删除OpenSSL

```
rm -rf /usr/lib/python2.7/site-packages/OpenSSL
rm -rf /usr/lib/python2.7/site-packages/pyOpenSSL-0.15.1.egg-info
```

### 下面安装OpenSSL时可能会出现这个错误
> ImportError: cannot import name 'SourceDistribution'

- 解决办法:手动升级pip

```
# cd tmp
# curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
# python get-pip.py
```
- 重新安装OpenSSL
```
pip install pyopenssl
```
### 回到群晖套件中心会提示python Module套件异常点击修复即可
![img](../img/post-img/2020/11/04/193783388.jpg)
