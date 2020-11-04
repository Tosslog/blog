---
layout:     post 
title:      "Docker Mongo 设置用户名密码"  #主标题
subtitle:   ""  #副标题
author:     "tosslog" 
header-img: "img/post-bg-miui6.jpg" #文章图片
#header-style: text #无图
hidden: false
catalog: true #标题跟随
tags: 
    - docker
    - mongodb
---

```
$ docker exec -it mongo mongo admin
# 创建一个名为 admin，密码为 123456 的用户。
db.createUser({ user:'admin',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'}]});
# 尝试使用上面创建的用户信息进行连接。
db.auth('admin', '123456')
# 创建超级用户
db.createUser({ user: "root" , pwd: "root", roles: ["root"]})
```