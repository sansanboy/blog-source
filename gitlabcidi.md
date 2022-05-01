---
title: gitlab持续集成步骤
date: 2019-05-29 23:56:54
tags:
---
公司有持续集成的系统，步骤为：
1. gitlab打tag
2. jenkins上选择tab进行构建部署
事件操作时需要很繁琐的步骤，要登gitlab，找到工程，找到tag菜单，填入tag名称，选择分支，生成tag。然后登录jenkins，选择工程，选择构建菜单，选择刚才的tag，点击构建。整个流程下来繁琐。
这个是在开发环境，生产环境更复杂，需要复制md5在申请部署页面填写。
那有没有更简洁的方法了，当然是gitlab ci/di

今天配置了一下，因为开发环境有自主权，步骤如下
1. 找一台机器安装gitlab runner
2. 注册runner到gitlab，需要在工程中生成地址和token。过程中需要选择部署的选项，很简单，按着步骤来就可以，会让写入需要登录的服务器，账号端口等
3. 第三步再工程中配置构建步骤
```shell
cd /application/blog
git checkout dev
git pull origin dev
```
开发环境默认为dev目录

4. 当工程有任何更新时都会触发任务去构建