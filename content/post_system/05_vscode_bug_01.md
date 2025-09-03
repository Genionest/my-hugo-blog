+++
date = '2024-07-17T17:12:00+08:00'
title = '修复ubuntu系统alt+tab切换vscode和浏览器时，鼠标滚轮错误的问题'
categories = ['vscode']
tags = ['ubuntu', 'vscode', 'browser']
cover = "/images/wallpaper8.jpg"
+++

## 问题描述

vscod和浏览器（如chrome）同时打开时，使用`alt+tab`切换窗口后，鼠标滚轮使用异常。

## 解决方案

git克隆以下项目，并执行以下命令，具体步骤参考[项目主页](https://github.com/lucasresck/gnome-shell-extension-alt-tab-scroll-workaround?tab=readme-ov-file#usage)
```bash
git clone https://github.com/lucasresck/gnome-shell-extension-alt-tab-scroll-workaround.git

cd gnome-shell-extension-alt-tab-scroll-workaround

make install
# 如果提示没有make
# su

# Restart the GNOME Shell:
# Press Alt+F2;
# Type r and press Enter.

# At this point, the extension should be enabled. If not:
make enable
```