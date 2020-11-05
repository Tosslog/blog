---
layout:     post 
title:      "github pages + jekyll 环境部署"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - github
    - jekyll
---
> ***博客使用的 github pages 对于大陆访问不太友好，如遇到内容缺失或是无法显示图片等问题，请科学访问！***

## 环境准备与安装

- 下载最新的ruby+devkit安装包 下载地址:[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)
- 安装rubyinstaller-devkit-2.7.2-1-x64

```
1. 安装rubyinstaller-devkit时一定要注意勾选添加环境变量与安装MSYS2。
2. 安装MSYS2时候选择3回车等待执行完毕即可。
3. 打开powershell 执行 gem install jekyll
4. 安装jekyll过程时候如果发生 not fount xxx 就 gem install xxx 然后在执行 gem install jeky 直到安装无报错。
```
## 运行 jekyll

```
1. 使用powershell cd 到项目所在路径
2. 执行命令：jekyll s 启动服务即可 127.0.0.1:4000 是访问地址
```
