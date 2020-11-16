---
layout:     post 
title:      "vscode 默认启动main.py"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - vscode
---

> 添加调试配置后在 launch.json 修改字段：
``` json 
"program": "${workspaceFolder}\\main.py"
```
