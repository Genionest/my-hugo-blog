+++
date = '2023-07-28T05:04:00+08:00'
title = 'python包管理工具uv'
categories = ['python']
tags = ['python', 'uv']
cover = "/images/wallpaper1.jpg"
+++


## 官方文档
[官网](https://docs.astral.sh/uv/#highlights)

## 如何安装 UV
有几种常用的安装方式：

### 独立安装脚本 (推荐):

macOS / Linux:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows (PowerShell):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

这种方式会自动下载并安装 UV，同时也会将 UV 路径添加到你的环境变量中。

通过 Homebrew (macOS / Linux):

```bash
brew install uv
```

### 通过 pip (不推荐用于生产环境):

```bash
pip install uv
```

虽然可以通过 pip 安装 UV，但官方不推荐这种方式，因为它可能导致一些环境管理上的复杂性。

安装完成后，你可以运行 

```bash
uv version
```

来验证安装是否成功。

## UV 的基本使用
UV 的设计理念是提供一个更简洁、更快速的开发体验。以下是一些常用的命令示例：

### 1. 初始化项目与虚拟环境
如果你在一个新的项目目录中，可以这样初始化：

```bash
uv init
```
这会在当前目录创建一个 .venv 虚拟环境。

### 2. 安装依赖
安装单个包:

```bash
uv add requests
```

第一次运行 uv add 命令时，UV 会在当前工作目录创建一个新的虚拟环境，并安装指定的依赖。后续运行时，它会重用现有环境，并只安装或更新新请求的包。

安装指定版本:

```bash
uv add requests=2.1.2
```

从 requirements.txt 安装:
如果你有一个现有的 requirements.txt 文件，可以像 pip 一样安装：

```bash
uv pip install -r requirements.txt
```

安装可编辑模式的包:

```bash
uv pip install -e .
```

### 3. 运行脚本
你可以使用 uv run 来在项目的虚拟环境中运行 Python 脚本或命令，而无需手动激活虚拟环境：

```bash
uv run python your_script.py
```

或者直接运行一个命令：

```bash
uv run pytest
```

### 4. 管理 Python 版本 (可选)
UV 甚至可以帮助你安装和管理 Python 版本。

安装最新 Python 版本:

```bash
uv python install
```

安装特定 Python 版本:

```bash
uv python install 3.12
```

列出已安装的 Python 版本:

```bash
uv python list
```

UV 会自动下载所需的 Python 版本，并在其命令中自动使用它们。

### 5. 锁定依赖
UV 支持生成一个通用的锁文件 (uv.lock) 来精确地锁定项目的所有依赖及其版本，确保不同环境下的依赖一致性。

```bash
uv lock
```

这个命令会生成一个 uv.lock 文件。

根据锁文件同步环境：

```bash
uv sync
```

