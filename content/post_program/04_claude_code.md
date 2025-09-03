+++
date = '2024-08-29T06:22:21+08:00'
title = 'Claude Code'
categories = ['ai']
tags = ['ai']
cover = "/images/wallpaper4.jpg"
+++

## 下载
[claude code官网](https://docs.anthropic.com/en/docs/claude-code/quickstart)

首先需要[下载node.js18以上版本](https://nodejs.org/en/download/)

然后打开终端，输入以下命令：
```bash
npm install -g @anthropic-ai/claude-code
```
安装完成后，使用claude命令启动

## 使用
我们没有claude code的账户和api, 需要使用claude code router，
（claude code router是一个开源项目，可以让cladue code使用其他大模型的api），

安装claude code router, [github地址](https://github.com/musistudio/claude-code-router/blob/main/README_zh.md)
```bash
npm install -g @musistudio/claude-code-router
```
创建配置文件
```bash
mkdir ~/claude-code-router
vim ~/claude-code-router/config.json
```
输入以下内容，使用deepseek的api
```json
{
  "Providers": [
    {
      "name": "deepseek",
      "api_base_url": "https://api.deepseek.com/chat/completions",
      "api_key": "sk-5b4c22a13cb84cc09e5831ba4cb498a2",
      "models": ["deepseek-chat", "deepseek-reasoner"],
      "transformer": {
        "use": ["deepseek"],
        "deepseek-chat": {
          "use": ["tooluse"]
        }
      }
    }
  ],
  "Router": {
    "default": "deepseek,deepseek-chat",
    "think": "deepseek,deepseek-reasoner"
  }
}
```
启动claude code router
```bash
mkdir test  # 创建测试文件夹
cd test  # 进入测试文件夹，claude code会读取当前文件夹的文件
ccr code  # 启动claude code router
```
在输入框输入hello,如果有输出，说明配置成功

## vscode插件
在vscode上安装claude code for vscode插件

让vscode和claude code router打开同一个文件夹

在ccr的终端输入/ide回车，选择vscode，即可打通vscode和claude code router