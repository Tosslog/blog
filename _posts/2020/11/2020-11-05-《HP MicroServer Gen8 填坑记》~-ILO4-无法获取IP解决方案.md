---
layout:     post 
title:      "《HP MicroServer Gen8 填坑记》~ ILO4 无法获取IP解决方案"  #主标题
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
> 
***ILO无法获取IP有可能是突发性的***
比如：
1、运行中突然断电
2、通过hei群晖关机
3、升级ILO过程中断电
以上原因都有可能造成ILO挂掉（随机性的并不是百分百命中），有两个解决方案提供给大家

## 两种种修复方法
### 一、通过FTP上传ILO包与命令修复方法
iLO 网络刷新失败恢复
大多数固件升级可以成功完成。 如果在 iLO 固件升级期间服务器罕见地断电，在电力恢复后可
能会恢复 iLO。
在引导计算机时，内核将在主映像上执行映像验证。 如果映像已损坏或不完整，内核将进入“刷
新失败恢复”模式。 刷新失败恢复模式在 iLO 中激活 FTP 服务器。 通过该 FTP 服务器，可以将映
像发送到 iLO 以进行编程。 该 FTP 服务器不提供任何其它服务。
网络客户端可以连接到该 FTP 服务器。 连接的用户名为 test，密码为 flash。 要将固件映像发送
到 iLO，请使用 FTP 客户端 PUT 命令。 在收到映像后，iLO 将验证该映像。 如果映像是完整、
已签名且有效的固件映像，内核将开始对 FLASH 分区进行编程。
将映像完全写入 FLASH 分区后，通过向 iLO FTP 服务器发出 RESET 命令，重置 iLO。

```ftp
示例：
F:\ilo&gt;ftp 192.168.1.2
Connected to 192.168.1.2.
220 FTP Recovery server ready.
User (192.168.1.2:(none)): ftp
331 Password required.
Password:
231 Logged in.
ftp&gt; put iLO.bin
200 Ok.
150 ready for file
226-Checking file
226-File acceptable
226-Flashing 3% complete
226-Flashing 4% complete
226-Flashing 6% complete
.
.
.
226-Flashing 97% complete
226-Flashing 99% complete
226-Flashing 100% complete
226-Flashing completed
226 Closing file
ftp: 8388608 bytes sent in 1.38Seconds 6100.81 Kbytes/sec.
ftp&gt; quote reset
221 Goodbye (reset).
Connection closed by remote host.
ftp&gt; quit

```

### 二、刷SPP包解决
>SPP是什么？这个问题只能简单的概述一下SPP就像windows的SP1,SPP是惠普的补丁包，和windowsSP1不一样的是windowsSP1只是更新windows的补丁，而SPP包含了硬件更新的补丁其中就包括了ILO和BIOS的更新包，从而得知SPP包含了ILO补丁我们不妨试一下让他修复你已经挂掉的ILO！

此方法也有一些比较头疼问题，那就是去哪里下载SPP
官方需要在保修期内才能下载最新的SPP也就是说你的GEN8得在保修期内
获得SPP的包有三种方法
- 第一、难易程度：★
我们百度、谷歌、必应一下SPP看看有没有最新版的流出下载下来就行了
- 第二、难易程度：★★
就是给客服打电话，不要给HP打电话打了他也会让你打新华三集团客服！所以正确姿势是给新华三集团打电话！
让新华三给你派单产生一个服务号等待客服给你回电
接到电话后你可以直接向客服问能给个SPP下载地址吗？
如果你命好给了你地址后你就可以直接下载
如果命不好给了你地址后你得在保修期内才能下载
- 第三、难易程度：★（给钱都好办）
同样使用第二种方法给新华三打电话说你下无法下载SPP因为过保了，他会给你安排另一个人给你报价续保费用当时给我报价了续保1500包含当次的上门维修服务与配件更换维修，单次维修8000+当然我果断拒绝！如果你有是土豪当然你随意了。

好了上述三个得到spp方法已经说了
下面说一下如何使用SPP去救活你的ILO
将下载后的SPP做成U盘启动然后在关机状态插入U盘，开机引导进入SPP然后
选择“Automatic Firmware Update Version…..”，点击回车键“Enter”
系统先预读光盘信息
接着载入信息
屏幕左上方提示正在分析并随后进行自动安装
等待服务器自动重启即可
更新过程中可能会卡在白色界面不用管他等待 如果20分钟还没动 强制关机在引导一次
更新完成会提是失败的固件，再次从新更新spp
直到完全通过
此事你在此关机开机 会发现ILO出来了！
起死回生了！
