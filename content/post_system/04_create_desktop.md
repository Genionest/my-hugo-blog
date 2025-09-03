+++
date = '2024-07-17T17:25:00+08:00'
title = 'Ubuntu创建桌面快捷方式'
categories = ['ubuntu']
tags = ['ubuntu', 'desktop']
cover = "/images/wallpaper10.jpg"
+++

在Ubuntu系统中，一些软件不会自动创建快捷方式，需要我们手动创建。

Ubuntu系统中，到不需要创建快捷方式到桌面，在程序列表中能找出即可（双击win键即可显示程序列表）

以下是创建方式

```bash
# 确保目标程序可以执行，以app.AppImage为例
chmod +x path/app.AppImage

# 在/usr/share/applications下创建.desktop文件
cd /usr/share/applications

sudo vim app.desktop
```

app.desktop里输入以下内容并保存

```bash
[Desktop Entry]
Name=MyApp
Exec=/path/app.AppImage
Terminal=false
Type=Application
Icon=/path/app_img.png
StartupWMClass=MyApp
Categories=Tool
Comment=MyApp
```

一些软件需要在非沙盒模式下运行

```bash
[Desktop Entry]
Name=MyApp
Exec=/path/app.AppImage --no-sandbox %u
Terminal=false
Type=Application
Icon=/path/app_img.png
StartupWMClass=MyApp
Categories=Tool
Comment=MyApp
```

之后应该就可以看到对应的图标了，有时可能需要重启桌面环境（注销再登录）