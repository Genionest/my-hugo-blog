+++
date = '2024-07-17T16:58:00+08:00'
title = '双系统'
categories = ['ubuntu']
tags = ['ubuntu', 'windows', 'system']
cover = "/images/wallpaper6.jpg"
+++

### ubuntu镜像
下载[ubuntu镜像](https://ubuntu.com/download/desktop)(这里是24.04版本)

### 写入U盘工具
我们下载[图拉丁工具箱](https://www.tbtool.cn/download/index.html?t=1752741242532)，用里面的rufus，将镜像写入U盘。要选择uefi模式

### 安装uefi引导启动的windows
如果你的windows系统不是uefi引导启动的，需要重装为uefi引导启动。

准备一个8G以上的U盘，在里面安装一个uefi引导启动的windows系统。需要是uefi引导启动的

进入bios，把启动选项从legacy变为 仅uefi

进入pe，使用磁盘管理工具进行分区

这里使用DriverGenius，格式化系统盘，快速分区，格式要选择GPT(就是GUID格式)，只分一个就够了

这时会出现3个分区，e开头的和r开头的，还有一个主分区

看e开头的分区是字母还是数字盘符，如果是数字盘符，就格式化这个分区，给他指定一个字母盘符，选z（选啥都行，往后靠的话不会影响u盘、新加的硬盘、新增的分区）

使用cgi修复

### ubuntu安装

预装第三方软件可装可不装，装的话需要网络稳定

空间分配自己选择，可以按自己喜欢分配

我的方案：
- 启动盘1G
- swap分区(最好大于你的内存大小，我这里分配了24G)
- 根目录100G
- 剩下的都给/home

### 设置双系统启动

设置每次启动都经过grub2更新GRUB配置

bash
sudo update-grub

```bash
# 看是否有os-prober,没有要安装
sudo apt install os-prober
# 扫描系统
sudo os-prober
# 更新grub配置
sudo update-grub
# 也许能将windows扫出来, 扫不出来也没关系，有办法
# 扫出来会显示：Found Windows Boot Manager on /dev/nvme0
```
```bash
# 编辑grub配置文件
sudo vim /etc/default/grub

#####
# 修改相关参数
GRUB_TIMEOUT=20  # 设置菜单显示时间
GRUB_DISABLE_OS_PROBER=false  # 确保启用系统探测
#####

# 修改完后更新配置
sudo update-grub
```

如果上面windows没有扫出来，设置ubuntu系统优先启动，进入grub界面后，按esc键，然后输入exit命令，就会进入到windows里了

### 修改grub配置

打开终端，编辑GRUB配置文件：

```bash
sudo nano /etc/default/grub
```

找到以下参数并修改：

```bash
# 删除 "quiet splash" 以显示内核启动日志
GRUB_CMDLINE_LINUX_DEFAULT=""
# 可选：设置超时时间（单位：秒）
GRUB_TIMEOUT=5
```
- quiet：隐藏启动时的详细日志。
- splash：启用图形启动画面（ Plymouth ）。删除这两个参数可显示完整终端输出

更新GRUB配置

```bash
sudo update-grub
```

这样就可以在ubuntu启动时看到完整的启动日志了。