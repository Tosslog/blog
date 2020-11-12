---
layout:     post 
title:      "python 数组倒序"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - python
---

## 三种方式进行倒序

# 切片
```
print lists[::-1]
```
# 函数reverse 对数组进行操作
```
lists.reverse()

print lists
```
# 函数reversed 返回一个迭代对象，需要list化
```
print list(reversed(lists))
```