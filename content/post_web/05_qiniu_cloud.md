+++
date = '2025-07-23T01:05:56+08:00'
title = '七牛云'
categories = ['cloud']
tags = ['七牛云']
cover = "/images/wallpaper5.jpg"
+++

## 七牛云是个坑货，不要买
轻量服务器不能设置防火墙
好像还容易被封，跑路
总之别买

## 七牛云轻量服务器远程

点开七牛云的轻量服务器，点开详情，获取密码

使用ssh连接，用户名是root，密码在上面获取的密码

进去之后是root用户

## 安装docker

更新系统包
```bash
apt update
apt upgrade
```

安装docker
```bash
apt install docker.io
# 检查版本
docker version
```

安装docker-compose
```bash
apt install docker-compose
# 检查版本
docker-compose version
```

## 创建用户

创建普通用户
```bash
adduser username
passwd username
# 根据提示输入密码等信息
```

添加sudo权限
```bash
usermod -aG sudo username
# 验证是否成功
id username
grep username /etc/passwd
```

切换用户
```bash
su - username
```


