+++
date = '2024-07-17T17:12:00+08:00'
title = 'ubuntu非正常退出后解决办法'
categories = ['ubuntu']
tags = ['ubuntu']
cover = "/images/wallpaper7.jpg"
+++

## 问题描述

ubuntu系统在非正常退出后，下次启动时可能会出现错误

## 解决方法

开机时在 GRUB 菜单选择 **Advanced options for Ubuntu**, 
然后选择**Recovery mode**

在恢复模式菜单中依次选择 
- **fsck**（自动检查文件系统）
- **dpkg**（修复软件包）
- **grub**（更新引导配置）
- **clean** 
- **resume**（继续正常启动）。