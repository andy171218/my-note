## pacman&yay命令

**-S**

```bash

# 强行刷新一遍再更新
sudo pacman -Syyu
yay -Syyu

# 安装软件
sudo pacman -S 软件名
yay -S 软件名

# 搜索
sudo pacman -Ss 软件名
yay -Ss 软件名

# 清理缓存
sudo pacman -Sc
yay -Sc

```

**-R**

```bash

# 删除软件及其依赖，和全局配置文件
sudo pacman -Rns
yay -Rns

# 删除不再需要的依赖
sudo pacman -Rns $(pacman -Qdtq)
yay -Rns $(pacman -Qdtq)
```

**-Q**

```bash

# 查询所有安装的软件
sudo pacman -Q
yay -Q

# 查询安装了多少个软件
sudo pacman -Q | wc -l
yay -Q | wc -l

# 查询自己安装的软件
sudo pacman -Qe
yay -Qe

# 查询自己安装了多少个软件
sudo pacman -Qe | wc -l
yay -Qe | wc -l

# 整理自己安装的软件
sudo pacman -Qeq
yay -Qeq

# 查询具体软件
sudo pacman -Qs 软件名
yay -Qs 软件名

# 查询不再需要的软件依赖
sudo pacman -Qdt
yay -Qdt
```

### 习惯

每次关机的时候更新一下:`sudo pacman -Syyu`

定期清理缓存
