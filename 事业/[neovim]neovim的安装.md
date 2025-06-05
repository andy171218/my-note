## 在 Kali Linux 上安装 Neovim

Neovim 是 Vim 的一个现代化分支，具有更好的插件支持和更现代的架构。以下是在 Kali Linux 上安装 Neovim 的步骤：

### 使用 apt 安装（推荐）

```bash
# 首先更新软件包列表
sudo apt update

# 安装 Neovim
sudo apt install neovim -y
```

### 验证安装

```bash
# 检查 Neovim 版本
nvim --version
```

### 启动neovim

```bash
# 启动 Neovim
nvim
```

- :q - 退出
- :w - 保存
- :wq - 保存并退出
- i - 进入插入模式
- ESC - 退出插入模式

## Neovim的配置

### 安装 Nerd Fonts 到 Kali Linux (XFCE + zsh)

Nerd Fonts 是带有大量图标的字体补丁版本，非常适合终端使用。以下是安装步骤：

#### 1\. 创建字体目录

1. mkdir -p ~/.local/share/fonts
2. \# 在用户目录下创建字体存放目录
3. \# -p 参数确保父目录不存在时自动创建

#### 2\. 下载并安装 Nerd Fonts

1. \# <https://www.nerdfonts.com/font-downloads>
2. \# 下载第一个字体
3. \# 解压，然后把文件移动到~/.local/share/fonts

#### 3\. 更新字体缓存

1. fc-cache -fv
2. \# 更新系统字体缓存：
3. \# - -f 强制重建缓存
4. \# - -v 显示详细输出

#### 4\. 验证安装

1. fc-list | grep "xxx"
2. \# 检查字体是否安装成功
3. \# 应该能看到类似输出：/home/username/.local/share/fonts/xxxttf

#### 5\. 配置终端使用新字体

1. echo "你需要在终端设置中手动选择 xxx"
2. \# 打开终端设置 -> 外观 -> 字体
3. \# 选择 "xxx" 或类似名称

## Neovim的配置

## Neovim的使用

### lazyvim插件安装

i

1. \# required
2. mv ~/.config/nvim{,.bak}

4. \# optional but recommended
5. mv ~/.local/share/nvim{,.bak}
6. mv ~/.local/state/nvim{,.bak}
7. mv ~/.cache/nvim{,.bak}

9. git clone <https://github.com/LazyVim/starter> ~/.config/nvim

11. rm -rf ~/.config/nvim/.git

13. nvim
