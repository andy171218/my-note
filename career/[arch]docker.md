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
        "https://hub.rat.dev"
    ]
}

```

**重启服务**

```bash
sudo systemctl restart docker
```

**常用命令**

```bash
#!/bin/bash
# ======================
# Docker 镜像管理
# ======================

# 拉取镜像
docker pull ubuntu:22.04

# 列出本地镜像
docker images
# 带过滤条件查询
docker images --filter "dangling=true"  # 显示悬空镜像

# 删除镜像
docker rmi ubuntu:22.04
# 强制删除（即使有容器使用）
docker rmi -f ubuntu:22.04

# 构建镜像（需在 Dockerfile 所在目录执行）
docker build -t my-image:1.0 .

# 导出镜像到文件
docker save -o ubuntu_image.tar ubuntu:22.04

# 从文件导入镜像
docker load -i ubuntu_image.tar


# ======================
# Docker 容器管理
# ======================

# 创建并启动容器（-d 后台运行）
docker run -itd --name my-container ubuntu:22.04
# 带端口映射和卷挂载
docker run -d -p 8080:80 -v /host/path:/container/path --name web nginx:latest

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

# 查看容器日志
docker logs my-container
# 实时查看日志
docker logs -f my-container


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
cat my-container.tar | docker import - my-imported:1.0

# 完整备份容器（包含元数据）
docker commit my-container my-backup:1.0  # 先保存为镜像
docker save -o my-backup.tar my-backup:1.0  # 再导出镜像


# ======================
# 清理与维护
# ======================

# 删除所有停止的容器
docker container prune

# 删除所有悬空镜像
docker image prune

# 清理所有未使用资源（镜像/容器/网络）
docker system prune
# 强制清理（不确认）
docker system prune -f

# 查看磁盘使用情况
docker system df
```
