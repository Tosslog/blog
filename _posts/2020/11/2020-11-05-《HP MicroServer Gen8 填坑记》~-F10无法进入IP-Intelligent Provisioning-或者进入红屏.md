---
layout:     post 
title:      "《HP MicroServer Gen8 填坑记》~ F10无法进入IP（Intelligent Provisioning）或者进入红屏"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - Gen8
    - HP Gen8
    - HP MicroServer Gen8
---

>使用惠普IP修复工具修复即可
IP全称Intelligent Provisioning
下载HPIP的镜像然后写入USB镜像
关机状态下插入U盘开机启动引导镜像修复即可
具体操作也从网上拔了一些解决方案

- HP MicroServer Gen8通过iLO按F10键能进入 Intelligent Provisioning （之后简称IP）

![img](/img/post-img/2020/11/05/2445954562.jpg)

- 进入IP后我们就能配置gen8和安装系统了，操作非常简便。但是有一天我碰到了下图这样的情况。

![img](/img/post-img/2020/11/05/1888783258.jpg)

>当时我就懵了，没想到自带的程序还能坏掉，无奈之下上网求助吧。网上查询有人说冲刷BIOS就能好使，有人说重置磁盘阵列就能好使。对于HP MicroServer Gen8来说这两种说法都不对。
个人理解其实IP就是一个小的系统，出现上图那种情况就是他崩溃了。HP也意识到IP会出现崩溃，所以早早地就给出了解决方案。崩溃是可以修复的，在HP Intelligent Provisioning 用户指南中就有重装IP的介绍，不过由于步骤简单，篇幅较短（如下图）寥寥几行字。初学者或刚接触的人很难找到，而且网上也很少有这类的帖子，这也是我写这个帖子的初衷。

![img](/img/post-img/2020/11/05/2856825974.jpg)

重装步骤就像上图所述一样。IP的光盘和用户指南可以到这个链接: 
http://pan.baidu.com/s/1eQtlrSA
密码: r8we 
中HP Intelligent Provisioning Recovery Media文件夹下载，是iso的镜像文件。网盘的版本是1.62，能用，不过版本有些老，最新版本大家可以到官网去下载。
官网下载地址:[https://support.hpe.com/hpesc/public/km/product/5390291/Product#t=All&sort=relevancy&f:@kmswsoftwaretypekey=[swt8000194]](https://support.hpe.com/hpesc/public/km/product/5390291/Product#t=All&sort=relevancy&f:@kmswsoftwaretypekey=[swt8000194])

![img](/img/post-img/2020/11/05/3011417171.jpg)

2.XX的版本是给gen9用的，gen8系列的无法使用。

![img](/img/post-img/2020/11/05/2063317067.jpg)

直接在iLO加载光盘镜像，开机即可自动引导，不放心的可以手动进行光盘引导。

![img](/img/post-img/2020/11/05/1868028225.jpg)

下图就是引导成功后的安装界面。我仅在1.62安装的时候截了个图，界面都一样。

![img](/img/post-img/2020/11/05/2493630872.jpg)

安装完毕后会自动重启系统，1.63的IP进入后会有三个选项。选择第一个即可。

![img](/img/post-img/2020/11/05/427420913.jpg)

到此，IP就重装完成了，IP的升级过程也是这样。
希望此文对你有所帮助！

