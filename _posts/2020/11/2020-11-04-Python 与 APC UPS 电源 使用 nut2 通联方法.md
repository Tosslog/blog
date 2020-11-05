---
layout:     post 
title:      "Python 与 APC UPS 电源 使用 nut2 通联方法"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - apc usp
    - apc
    - usp
    - python
---
> ***博客使用的 github pages 对于大陆访问不太友好，如遇到内容缺失或是无法显示图片等问题，请科学访问！***


> 使用python 与 apc ups 通信

## 安装nut2包

``` pip
pip install nut2
```
## 使用方法
```python
from nut2 import PyNUTClient
client = PyNUTClient()
client.help()
client.list_ups()
client.list_vars("My_UPS")
```

