+++
date = '2023-07-17T00:53:00+08:00'
title = 'TeamSpeak3'
categories = ['service']
tags = ['teamspeak', '语音聊天']
cover = "/images/wallpaper3.jpg"
+++

### 部署teamspeak3服务器
docker部署teamspeak3服务器

在服务器运行以下命令
```bash
docker run --name=teamspeak-server \
  -p 9987:9987/udp \
  -p 10011:10011/tcp \
  -p 30033:30033/tcp \
  -e TS3SERVER_LICENSE=accept \
  teamspeak
```

之后会打印一串文字

注意，找到Important Info，把里面的信息保存起来，里面应该有 管理员用户名，密码，key

然后继续往下，找到token，把token也保存起来

如果没有显示文字，通过下面命令查看
```bash
docker logs teamspeak-server | grep "ServerAdmin privilege key"
```

云服务器记得设置防火墙开放对应的端口，udp:9987，tcp:10011，tcp:30033

### teamspeak3客户端
进入teamspeak官网[下载](https://teamspeak.com/en/downloads/#ts3client)

如果是ubuntu系统，下载会得到一个TeamSpeak3-Client-linux_amd64.run文件

按照以下方式进行安装
```bash
mkdir ~/softwares/teamspeak
# 将TeamSpeak3-Client-linux_amd64.run文件放入里面
cd teamspeak
chmod +x TeamSpeak3-Client-linux_amd64.run
./TeamSpeak3-Client-linux_amd64.run # 不要sudo
# 然后会输出一大段文字，最后会让你输入y，
# 然后就会在当前目录创建一个TeamSpeak3-Client-linux_amd64文件夹
```

启动teamspeak客户端
```bash
# 进入TeamSpeak3-Client-linux_amd64文件夹
.\ts3client_runscript.sh
```

### 连接服务器
启动客户端后，点击左上角的connections按钮

在弹出的窗口中，输入服务器的ip地址，点击connect按钮即可

如果提示需要privilige key，就把之前保存的token复制进去即可（token只能被一个用户注册，不过进去之后可以给其他人管理员权限）