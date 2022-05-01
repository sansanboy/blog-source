---
title: nginx配置模版
date: 2019-05-29 00:59:07
tags:
---
公司统一应用的配置，要求每个应用都要有自己的appid，重新部署，规范化。自己的项目差不多有10个，都是php项目，配置基本一样。配置nginx的时候传统的做法是vim每个nginx配置文件进行配置。这个完全可以自定化，可以写一个配置模板，里面的appid和端口用变量替换。然后用sed命令进行批量替换。
- 配置模板
```
upstream {appid}_server {
        server *.*.*.*:{port} weight=10 max_fails=2 fail_timeout=20;
}
```
- 运行脚本 *new.sh*
```
#!/bin/bash
APPID=$1
PORT=$2
cp demo.conf $APPID.conf
sed -i 's/{appid}/'"$APPID"'/g' $APPID.conf
sed -i 's/{port}/'"$PORT"'/g' $APPID.conf
```
- 运行
```
sh new.sh blog 21800
```
运行之后会根据一个模板生成新的配置文件，里面的端口和对应的appid会自动替换掉。
以前看到有人做成网页的，根据选项生产nginx配置文件。 
