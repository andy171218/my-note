

### docker简介

Docker 是一个开源的 ​​容器化平台​​，用于开发、部署和运行应用程序。它通过 ​​容器（Container）​​ 技术，将应用程序及其依赖项打包成轻量级、可移植的单元，实现 ​​"一次构建，随处运行"​​。

### docker安装

```bash
sudo pacman -S docker
```

### docker使用

**启动docker服务**

```bash
sudo systemctl enable --now docker
```

**将当前用户加入docker组(避免每次都使用sudo)**

```bash
sudo usermod -aG docker $USER
newgrp docker  # 立即生效
```

**创建配置文件**

```bash
sudo mkdir -p /etc/docker
sudo nvim /etc/docker/daemon.json
```

**配置镜像**
```bash
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io",
        "https://docker.1panel.live",
        "https://hub.rat.dev",
        "https://elastic.m.daocloud.io",
        "https://gcr.m.daocloud.io",
        "https://ghcr.m.daocloud.io",
        "https://k8s-gcr.m.daocloud.io",
        "https://k8s.m.daocloud.io",
        "https://mcr.m.daocloud.io",
        "https://nvcr.m.daocloud.io",
        "https://quay.m.daocloud.io",
        "https://ollama.m.daocloud.io"
    ]
}
```

**重启服务**

```bash
sudo systemctl restart docker
```

**docker_image_pusher**

**settings:**

![image-20250717153129158](.\assets\image-20250717153129158.png)



**阿里云:**

![image-20250717153358181](.\assets\image-20250717153358181.png)



![image-20250717153536545](.\assets\image-20250717153536545.png)

**Actions:**

![image-20250717153751836](.\assets\image-20250717153751836.png)



![image-20250717153820378](.\assets\image-20250717153820378.png)

**添加镜像:**

![image-20250717153834222](.\assets\image-20250717153834222.png)

**最后:**

![image-20250717153920704](.\assets\image-20250717153920704.png)

![image-20250717154017837](.\assets\image-20250717154017837.png)

**常用命令**

```bash
# ======================
# Docker 镜像管理
# ======================

# 拉取镜像
docker pull ubuntu:22.04

# 列出本地镜像
docker images

# 删除镜像
docker rmi ubuntu:22.04
# 强制删除（即使有容器使用）
docker rmi -f ubuntu:22.04

# 构建镜像（需在 Dockerfile 所在目录执行）
docker build -t my-image:1.0 .

# 导出镜像到文件(指定名称和版本号)
docker save -o ubuntu_image.tar ubuntu:22.04

# 从文件导入镜像
docker load -i ubuntu_image.tar


# ======================
# Docker 容器管理
# ======================

# 创建并启动容器（-d 后台运行） --name:起名
docker run -d --name my-container ubuntu:22.04
# --restart=always 重启自动启动该容器
docker run -d --restart=always --name my-container ubuntu:22.04

# 带端口映射和卷挂载
# -p:8080:80  主机端口:容器端口  访问主机端口及能访问到容器应用 -v 主机目录:容器目录 将主机的目录挂载到容器内
docker run -d -p 8080:80 -v /host/path:/container/path --name web nginx:latest

# -e 设置容器内的环境变量，这里是配置 MySQL 的 root 用户密码。 不指定端口:在容器群内使用,外部主机无法访问
docker run --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7

# --link 目标容器名称（之前运行的 MySQL 容器名）:在 WordPress 容器内的别名（用于配置文件中）
# 作用：将当前 WordPress 容器连接到名为 mysql的容器，并设置别名 mysql

docker run -d --link mysql:mysql -p 86:80 wordpress:5.6

# 列出运行中的容器
docker ps
# 列出所有容器（包括停止的）
docker ps -a

# 启动/停止/重启容器
docker start my-container
docker stop my-container
docker restart my-container

# 进入运行中的容器（交互模式）
docker exec -it my-container /bin/bash

# 删除容器
docker rm my-container
# 强制删除运行中的容器
docker rm -f my-container
# 强制删除所有容器 -q:只显示id号
docker rm -f `docker ps -a -q`

# 查看容器进程
docker top ID

# 查看容器资源占用情况
docker stats ID

# 查看容器日志
docker logs my-container
# 实时查看日志
docker logs -f my-container

# 查看容器端口映射
docker port ID

# 查看容器IP地址
docker inspect -f '{{.Name}} => {{.NetworkSettings.IPAddress}}' $(docker ps -aq)


# ======================
# 数据管理与备份
# ======================

# 从容器复制文件到主机
docker cp my-container:/path/in/container /host/path

# 从主机复制文件到容器
docker cp /host/path my-container:/path/in/container

# 将容器保存为新镜像
docker commit my-container my-snapshot:1.0


# ======================
# 备份与恢复
# ======================

# 导出容器文件系统（不包含历史记录）
docker export -o my-container.tar my-container

# 从导出文件创建新镜像
docker import my-container.tar my-imported:1.0

# 完整备份容器（包含元数据）
docker commit my-container my-backup:1.0  # 先保存为镜像
docker save -o my-backup.tar my-backup:1.0  # 再导出镜像

# 查看磁盘使用情况
docker system df
```


### docker-compose

docker-compose 是一个用来管理docker容器的工具,可以很方便的用来管理多个容器



```zsh
# 安装docker-compose
sudo pacman -S docker-compose

# 配置docker-compose.yml文件
# 创建对应的文件夹
mkdir xxx
cd xxx/
touch docker-compose.ym1
vim docker-compose.yml

# 配置文件内容
version: '3.5'

services:
  nginx:
    container_name: nginx
    image: nginx:1.25.4
    environment:
      - NGINX_HOST=foobar.com
      - NGINX_PORT=80
    volumes:
      - ${DOCKER_VOLUME_DIRECTORY:-.}/data:/usr/share/nginx/html
      - ${DOCKER_VOLUME_DIRECTORY:-.}/config/nginx.conf:/etc/nginx/nginx.conf
      - ${DOCKER_VOLUME_DIRECTORY:-.}/templates:/etc/nginx/templates
    ports:
      - "80:80"
networks:
  default:
    name: nginx

# 命令
#创建并启动
docker-compose up-d #启动之后就可以通过浏览器访问了
#停止并删除
docker-compose down
#重启
docker-compose restart
#停止
docker-compose stop
#启动
docker-compose start
```









