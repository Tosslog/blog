---
layout:     post 
title:      "免费泛域名SSL证书Let's Encrypt自动申请并定时更新证书"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - SSL
    - Let's Encrypt
    - 证书
---

## 什么是 SSL 证书？
SSL 是保护用户数据和防止身份被盗用的最佳方式。拥有 SSL 证书的网站可以告诉用户，他们可以放心的浏览，SSL 可以保护他们的数据安全。不同的 SSL 证书提供不同级别的验证。了解更多 
目前比较火的适合个人用户的证书就是 Let’s Encrypt，这货是免费的，下面我们就介绍一下如何在 Linux 服务器上配置 SSL 证书

免费证书服务商：Let's Encrypt
证书有效周期：90天
优点：免费
缺点：90天更新一次
本次介绍使用系统：centos7
所需插件：acme.sh，crontab
所需域名：哪里申请的都可以，本次使用（阿里做演示因为我只有阿里的。。。。）

## 下面开始操作
使用 acme.sh 安装 Let’s Encrypt 证书
Let’s Encrypt 提供很多方式，网上也有不少教程，但是都不方便操作，下面我们就介绍一款国人写的开源脚本 acme.sh
首先，进入服务器后获取 acme.sh 脚本，此操作不一定需要 root 用户登陆

使用 curl 方式获取，系统需要安装 curl 软件
```shell
# curl https://get.acme.sh | sh
``` 
你也可以使用 wget 方式
```shell
# wget -O - https://get.acme.sh | sh
```
以上两种方法建议挂代理下载！！！
安装过程中可能会出现提示 红色字体 提到了一些环境你需要安装
如 socat，crontab
如果出现提示那就直接 yum install  安装上面两个所需要的东西就好了！
然后重新执行一次 curl 或者wget

安装完成后在根目录下运行 acme.sh
正常应该会出现 help的命令参数说明
如出现
```shell
bash: acme.sh: command not found
```
无法找到acme.sh命令时请运行下面蓝色代码！
```shell
source ~/.bashrc
```
在次根目录下运行acme.sh 检测是否成功出现帮助说明！
安装好后所有的路径都会给你呈现出来，默认路径是隐藏的！
```shell
# root/.acme.sh/
```
## 下面开始配置文件
之前说过使用的是阿里域名所以阿里域名的同学请先去申请你的后台key，Secret不会的给阿里打电话手把手教你操作！
key，secret 需要去配置文件中配置
配置文件路径在默认目录下有个叫account.conf的文件
```shell
# vim account.conf
# 会出现下面的文件信息

#LOG_FILE="/root/.acme.sh/acme.sh.log"
#LOG_LEVEL=1
#AUTO_UPGRADE='1'
#NO_TIMESTAMP=1
改成下面所示
#LOG_FILE="/root/.acme.sh/acme.sh.log"
#LOG_LEVEL=1
#AUTO_UPGRADE='1'
#NO_TIMESTAMP=1
export Ali_Key="你申请的key"
export Ali_Secret="你申请的sceret"
配置完毕然后保存退出！
```
下面开始申请证书
在根目录下运行如下脚本
```shell
#　acme.sh --issue --dns dns_ali -d xxx.com -d *.xxx.com
-d 顺序不要乱 不然可能会出问题
xxx.com是要换成你自己的域名
*代表泛域名
```
下面是运行输出
```shell
./apply_acme.sh: line 1: !/bin/bash: No such file or directory
[Fri Dec 21 08:05:07 UTC 2018] Domains have changed.
[Fri Dec 21 08:05:07 UTC 2018] Multi domain='DNS:baidu.com,DNS:*.baidu.com,DNS:*.kkk.baidu.com'
[Fri Dec 21 08:05:07 UTC 2018] Getting domain auth token for each domain
[Fri Dec 21 08:05:13 UTC 2018] Getting webroot for domain='baidu.com'
[Fri Dec 21 08:05:13 UTC 2018] Getting webroot for domain='*.baidu.com'
[Fri Dec 21 08:05:13 UTC 2018] Getting webroot for domain='*.kkk.baidu.com'
[Fri Dec 21 08:05:13 UTC 2018] Found domain api file: /root/.acme.sh/dnsapi/dns_ali.sh
[Fri Dec 21 08:05:18 UTC 2018] Sleep 120 seconds for the txt records to take effect
[Fri Dec 21 08:07:20 UTC 2018] baidu.com is already verified, skip dns-01.
[Fri Dec 21 08:07:20 UTC 2018] *.baidu.com is already verified, skip dns-01.
[Fri Dec 21 08:07:20 UTC 2018] Verifying:*.kkk.baidu.com
[Fri Dec 21 08:07:23 UTC 2018] Success
[Fri Dec 21 08:07:23 UTC 2018] Removing DNS records.
[Fri Dec 21 08:07:31 UTC 2018] Verify finished, start to sign.
[Fri Dec 21 08:07:33 UTC 2018] Cert success.
-----BEGIN CERTIFICATE-----
此处为证书加密片段由于过多有涉及隐私就不贴出来了
-----END CERTIFICATE-----
[Fri Dec 21 08:07:33 UTC 2018] Your cert is in /root/.acme.sh/baidu.com/inas.wiki.cer 
[Fri Dec 21 08:07:33 UTC 2018] Your cert key is in /root/.acme.sh/baidu.com/inas.wiki.key 
[Fri Dec 21 08:07:33 UTC 2018] The intermediate CA cert is in /root/.acme.sh/baidu.com/ca.cer 
[Fri Dec 21 08:07:33 UTC 2018] And the full chain certs is there: /root/.acme.sh/inas.wiki/fullchain.cer 
[Fri Dec 21 08:07:33 UTC 2018] Installing key to:/etc/nginx/ssl/inas.wiki.key
[Fri Dec 21 08:07:33 UTC 2018] Installing full chain to:/etc/nginx/ssl/inas.wiki.cer
[Fri Dec 21 08:07:33 UTC 2018] Run reload cmd: service nginx restart
Redirecting to /bin/systemctl restart nginx.service
[Fri Dec 21 08:07:34 UTC 2018] Reload success
```
运行过程整个需要120+秒
如果运行之后有出现红色字体说明有些问题你需要去解决
如果都是有很多绿色的字说明OK了！申请证书完成！
运行成功后会提示你的证书在哪个目录下
默认会在
```shell
root/.acme.sh/你域名目录下
```
最后一步安装证书！说白了就是复制一下证书到你的 nginx/ssl目录下
```shell
acme.sh --installcert -d xxx.com \
--key-file /etc/nginx/ssl/xxx.com.key \
--fullchain-file /etc/nginx/ssl/xxx.com.cer \
--reloadcmd "service nginx restart"
```
apply_acme.sh是我自己写的执行脚本懒得以后有修改的时候每次都一行一行敲最后脚本内容如下
有需要的朋友可以借拿走
```shell
# !/bin/bash -v
# root/.acme.sh/acme.sh --issue --dns dns_ali -d baidu.com -d *.baidu.com-d *.kkk.baidu.com
# root/.acme.sh/acme.sh --installcert -d baidu.com \
--key-file /etc/nginx/ssl/baidu.com.key \
--fullchain-file /etc/nginx/ssl/baidu.com.cer \
--reloadcmd "service nginx restart"
```

## 最后说一些其他的小事项
证书自动更新
目前证书在 60 天以后会自动更新, 你无需任何操作. 今后有可能会缩短这个时间, 不过都是自动的,
你不用关心.

更新acme.sh
目前由于 acme 协议和 letsencrypt CA 都在频繁的更新, 因此 acme.sh 也经常更新以保持同步.
```shell
升级 acme.sh 到最新版 :
# acme.sh --upgrade
如果你不想手动升级, 可以开启自动升级:
# acme.sh --upgrade --auto-upgrade
之后, acme.sh 就会自动保持更新了
你也可以随时关闭自动更新:
# acme.sh --upgrade --auto-upgrade 0
```
整体的一套流程终于敲完了 算是做个详细备忘吧！
