---
layout:     post 
title:      "PLEX webhooks for python + flask"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - python
    - flask
    - plex
    - webhooks
---
> ***博客使用的 github pages 对于大陆访问不太友好，如遇到内容缺失或是无法显示图片等问题，请科学访问！***


## 可触发的事件

``` 
library.on.deck
添加了新项目，该项目显示在用户的“甲板上”。此活动还附有海报。

library.new 
将新项目添加到用户有权访问的库中。此活动还附有海报。

media.pause
媒体播放暂停。

media.play
媒体开始播放。附有适当的海报。

media.rate
媒体已评级。此活动还附有海报。

media.resume 
媒体播放恢复。

media.scrobble 
已查看媒体（播放超过90％标记）。

media.stop 
媒体播放停止。

服务器所有者
这些事件仅针对服务器所有者/管理员帐户发送，并且通常与服务器上的事件有关。

admin.database.backup 
通过计划任务成功完成了数据库备份。

admin.database.corrupted 
在服务器数据库中检测到损坏。

device.new 
设备出于任何原因访问所有者的服务器，这可能来自后台连接测试，并不一定表示活动的浏览或回放。

playback.started
回放由服务器的共享用户启动。此活动还附有海报。

```

## 使用方法
> 编写python flask 处理

``` python
#! /usr/bin/env python
# -*- coding: utf-8 -*-

import requests
from flask import *
import os
from datetime import timedelta
import json
import base64

app = Flask(__name__)

@app.route('/webhook', methods=['POST'])
def webhooksEvent():
    
    if request.method == 'POST':
        plex_dict = request.form.to_dict()
        inner_data = plex_dict["payload"]
        inner_data = json.loads(inner_data)
        event = inner_data["event"]
        media_type = inner_data["Metadata"]["type"]
        local = inner_data["Player"]["local"]
        device = inner_data["Player"]["title"]
        '''
        处理代码..........
        '''

if __name__ == '__main__':
    app.run(
        host='0.0.0.0',
        port=1000,
        debug=False
    )
```
