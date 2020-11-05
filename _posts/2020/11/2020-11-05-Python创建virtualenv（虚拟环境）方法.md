---
layout:     post 
title:      "Python创建virtualenv（虚拟环境）方法"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - virtualenv
    - venv
    - python
    - 虚拟环境
---
> ***博客使用的 github pages 对于大陆访问不太友好，如遇到内容缺失或是无法显示图片等问题，请科学访问！***


## 通常创建虚拟环境命令是
```
virtualenv venv
```

## 下面修改成如下命令

```
virtualenv -p c:\Python27\python2.exe venv2
virtualenv -p c:\Python37\python3.exe venv3
```
***其中python3.exe与2.exe 是为了共存特意修改区分***




