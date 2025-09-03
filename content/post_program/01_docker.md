+++
date = '2024-07-17T13:55:00+08:00'
title = 'Docker'
categories = ['docker']
tags = ['ubuntu', 'docker']
cover = "/images/wallpaper5.jpg"
+++

### 安装Docker

[安装教程](https://docs.docker.com/engine/install/ubuntu/)

### 常用命令

```bash
docker ps  # 查看运行的容器
docker ps -a  # 查看所有容器
docker rm container-name  # 删除容器
docker images  # 查看所有镜像
docker rmi image-name  # 删除镜像
```

### 构建镜像

```bash
docker build -t image-name:latest /path/
# -t 制定tag, latest就是tag
```

### 创建并运行容器

```bash
docker run -d -p 5000:5000 --name container-name image-name
# -d detached 后台运行 
# -p 端口映射 (主机端口：容器端口)
# --name 为容器指定名称，不指定docker会随机制定名字
```

### 数据持久化

```dockerfile
docker run \
  --name container-name \
  -p 3307:3306 \
  -v mysql_data:/var/lib/mysql \
  image-name
# -v 数据标签:对应容器内数据的路径
```

数据卷操作

```bash
docker volume ls  # 查看所有数据卷
docker volume rm volume-name  # 移除数据卷
```

### 容器执行命令行

```bash
docker exec -it container-name 你的命令行
# -i/--interactive 保持STDIN打开，即使没有附加
# -t/--tty 分配一个伪终端
# -d/--detach 在后台运行
# -e 设置环境变量
# -w 设置工作目录
```

### 容器间通信

```yml
version: '3.8'

services:
  mysql_app:
    image: mysql:8.0
    ...
    ports:
      - "3307:3306"  # 这里是本机端口被占用了，写的3307,不然可以写3306
        # mysql默认使用的是3306端口，这里这是暴露端口，修改这个不会改变mysql端口
    ...
    networks:
      - app-network  # 网络分组

  app:
    build: ./backend
    environment:
      DB_PORT: 3306  # 这里是设置环境变量，这程序里获取，填充
    networks:
      - app-network  # 网络分组

networks:
  app-network:
    driver: bridge  # 连接方式
```

### 一些问题

- docker下载python一些比较大的第三方库时，可能会导致超时，使用国内的pypi镜像源可以降低下载时间
- ubuntu24.04安装docker-desktop会有问题，最好不要安装
- ubuntu24.04如果安装了docker-desktop无法使用，请按照[官方文档](https://docs.docker.com/desktop/uninstall/)进行卸载，

  如果还是无法正常使用，尝试以下方法
  ```bash
    docker buildx ls
    # 查看是否有desktop-linux，并且错误
    # 如果有
    docker buildx rm desktop-linux
    # 如果还是报错，可以尝试ai搜索下
    # 这里解决问题的办法是,删除~/.docker文件，重建，删除文件前最好备份
    mv ~/.docker ~/.docker_backup_$(date +%Y%m%d%H%M%S)
    # 重建一个空的
    mkdir ~/.docker

    # 重新初始化
    docker buildx install
    docker context use default
  ```
