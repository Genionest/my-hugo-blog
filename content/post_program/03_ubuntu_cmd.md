+++
date = '2024-08-12T06:22:00+08:00'
title = 'ubuntu上好用的命令'
categories = ['ubuntu']
tags = ['ubuntu']
cover = "/images/wallpaper3.jpg"
+++

## scp:远程传输文件
```bash
scp -P 端口号 文件路径 用户名@服务器IP:目标文件路径
# 例如
scp -P 33060 /home/wang/test.txt liu@192.168.1.1:/home/liu/
# 之后会提示输入用户的密码
```

## du:统计文件夹大小
```bash
du -sh 文件路径 
# -s 表示汇总，没有-s则会显示所有子文件夹的大小
# -h 表示以K,M,G为单位显示
```

## gio trash:移动文件到回收站
```bash
gio trash 文件路径          # 移动到回收站
gio trash --list      # 查看回收站
gio trash --empty       # 清空回收站
gio trash --restore 文件路径  # 恢复文件
```

## find:查找文件
```bash
find / -name "文件名"
```

## nmap:扫描端口
```bash
nmap IP地址
nmap -p 端口号 IP地址
nmap -p 400-4000 IP地址  # 范围扫描端口
```