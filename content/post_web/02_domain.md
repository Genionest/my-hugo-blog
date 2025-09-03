+++
date = '2024-07-14T22:48:31+08:00'
title = '域名购买与相关配置'
categories = ['website']
tags = ['domain', 'DNS', 'CA', 'cloudeflare']
cover = "/images/wallpaper2.jpg"
+++

### 域名购买
[spaceship](www.spaceship.com)
购买便宜域名
我们可以输入一个6位数字.xyz的域名，一般能够得到一个便宜的域名。
[视频教程](https://b23.tv/LnWCQhJ)（前半部分）

### 域名托管到cloudeflare
然后我们将其托管到cloudflare上，使用cloudflare的DNS解析服务。
[视频教程](https://b23.tv/LnWCQhJ)（后半部分）


### 安全证书、ssl/tls、https
然后配置安全证书以实现HTTPS访问和SSL传输  

在cloudeflare点击你的域名，进入域名界面  

域名界面->SSL/TLS->概述->配置->选择灵活，保存
（灵活是域名—>cloudeflare是https,cloudeflare->服务器是http）
（完全是整个过程都是http,但是需要服务器部署证书，cloudeflare默认给的证书不能实现）

域名界面->边缘证书->始终使用https 开启
[视频教程](https://b23.tv/mVmDeHV)（视频的末尾部分）

### 域名绑定到服务器IP
域名界面->DNS->添加记录

类型选择A, (类型选择AAAA是ipv6地址的配置方式)

如果你的域名是abc.xyz，
名称选@, 就是abc.xyz，
名称选www, 就是www.abc.xyz

IPV4就是你服务器的ip地址
[视频教程](https://b23.tv/vBvvk88)
