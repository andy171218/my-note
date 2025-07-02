## Timeshift 是什么？

Timeshift 是一个系统备份和恢复工具，类似于 Windows 的系统还原功能。它通过创建系统快照来保护你的系统，当系统出现问题时可以恢复到之前的健康状态。

### 安装 Timeshift

```bash
sudo pacman -S timeshift
```

### 文件系统要求

Timeshift 对不同文件系统的支持情况：

- **Btrfs**：原生支持，效率最高
- **ext4**：通过 rsync 方式支持
- 其他文件系统：通过 rsync 方式支持

### 使用Timeshift

打开timeshift,根据提示一步步操作:
选择快照类型:Btrfs
选择快照位置:默认位置
选择快照频率:每周,3个
(不建议)是否包含home目录:是

```bash
# 启动定时任务让timeshift可以自动创建快照
sudo systemctl enable --now cronie.service

# 然后按照步骤一步步来即可
# 恢复系统
sudo timeshift --list
sudo timeshift --restore
```
