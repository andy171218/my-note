### distrobox简介

Distrobox 是一个基于 ​​Podman/Docker​​ 的轻量级工具，用于创建和管理 ​​持久化的 Linux 发行版容器​​。它允许你在一个主机上运行多个不同的 Linux 发行版（如 Ubuntu、Arch、Fedora），并深度集成到你的系统中。

### distrobox安装

```bash
sudo pacman -S distrobox
```

### distrobox使用

```bash
# ======================
# Distrobox 容器管理
# ======================

# 创建容器（默认使用 Fedora）
distrobox create --name my-container --image fedora:latest

# 使用自定义镜像创建容器（Ubuntu 22.04）
distrobox create --name dev-ubuntu --image ubuntu:22.04

# 进入容器
distrobox enter my-container

# 列出所有容器
distrobox list

# 停止容器
distrobox stop my-container

# 删除容器
distrobox rm my-container

# 更新容器内所有软件包
distrobox upgrade my-container
distrobox upgrade --all  # 更新所有容器

# 退出容器
exit

# ======================
# 镜像与导出操作
# ======================

# 从容器导出应用到宿主机（例如导出 VSCode）
distrobox export --app code --bin code my-container

# 在容器内导出命令到宿主机（需在容器内执行）
distrobox-export --bin /usr/bin/htop


# ======================
# 备份与恢复
# ======================

# 导出容器备份
distrobox export --backup my-container --backup-file my-backup.tar

# 从备份恢复容器
distrobox import --backup-file my-backup.tar

```
