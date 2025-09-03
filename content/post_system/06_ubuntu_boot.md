+++
date = '2024-07-31T04:07:00+08:00'
title = 'ubuntu引导修复,修复grub'
categories = ['ubuntu']
tags = ['ubuntu']
cover = "/images/wallpaper6.jpg"
+++

## 背景
之前买了各移动硬盘，在里面装了个Ubuntu系统

因为我之前已经在电脑上装了一个Ubuntu系统，所以现在进入grub后默认是后装的Ubuntu系统
（也就是移动硬盘Ubuntu）

更重要的是，当我把移动硬盘拔掉后，电脑就找不到Ubuntu的启动项了，会直接进入Windows
（我的电脑是Ubuntu和Windows双系统）

## 解决办法
我在网上查了一些解决办法，一个是修复grub，具体步骤如下（事先声明：这个方案对我的问题没用）

进入Live CD，需要联网，然后下载boot-repair，运行，点击Recommended repair
```bash
sudo add-apt-repository ppa:yannubuntu/boot-repair
sudo apt update
sudo apt install boot-repair
boot-repair
```

这是软件的方法，还有手动修复的方法，这里不做介绍，因为我的问题不是这个，
我也无法判断手动的方法是否有效

但正如我之前说了，这个方法在我这里没用

所以我找到了另外一个方法

## 解决办法2
这里我们要进入bios里进行设置，我的电脑是dell g15, 不同的电脑可能不一样

进入bios后，找到boot选项，找到add boot option, 

进去之后，会看到一个ESP分区，但那个不是，我们需要找到之前的Ubuntu启动项，
它的名字带有Volume，看不出来是什么，但点开之后，会发现有efi选项，继续点开，
会发现有ubuntu选项，继续点开，选择里面的grubx64.efi

之后我们需要为它命名，就叫UbuntuBoot吧，然后就可以点击add boot option了

之后，将UbuntuBoot设置为第一启动项，重启电脑

之后就成功了，可以正常启动之前安装的Ubuntu了，😭😭😭，折腾了好久

