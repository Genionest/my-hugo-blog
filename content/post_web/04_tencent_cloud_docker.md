+++
date = '2024-07-17T01:07:00+08:00'
title = '腾讯云安装Docker'
categories = ['docker']
tags = ['腾讯云', 'docker']
cover = "/images/wallpaper4.jpg"
+++

### 远程登陆腾讯云
首先修改腾讯与的密码，用户名那里不要改，就保持为ubuntu

然后使用远程工具， ssh连接，后面会让你输入密码，输入就行了

ubuntu上可以使用remmina，windows可以使用xshell

### 安装Docker
这里选用的系统是ubuntu24.0.4 LTS

更新系统，重启
```bash
#切换到root用户
sudo -s
cd ~
#更新
sudo apt update
sudo apt upgrade
#重启
reboot
```

```bash
# 不安装docker,而是安装docker.io
sudo apt install docker.io
# 检查docker版本
docker version  # 可能需要sudo
# 安装docker-compose
sudo apt install docker-compose
# 检查docker-compose版本
docker-compose version  # docker-compose不可用，换成docker compose
```
如果想要安装docker而不只是docker.io，则可以按照以下步骤进行安装，感觉没区别

前置准备
```bash
#可以按照docker官网的内容卸载原本安装的docker
#安装gnome-terminal
sudo apt install gnome-terminal
#安装curl
#检查curl是否安装
whereis curl
#没有则需要安装
sudo apt install curl
```

安装Docker
```bash
# 安装docker
sudo apt install docker
# 检查docker版本
docker version  # 可能需要sudo

# 安装docker-compose
sudo apt install docker-compose
# 检查docker-compose版本
docker-compose version  # docker-compose不可用，换成docker compose
```

按照提示进行测试hello-world即可