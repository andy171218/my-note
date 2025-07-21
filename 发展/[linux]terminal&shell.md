### terminal配置

**kitty的安装**

```zsh
sudo pacman -S kitty
```

**kitty的配置**

重载配置:`ctrl+shift+f5`
主题:`kitty +kitten themes`
字体:`kitty list-fonts --psnames`

```zsh
# ~/.config/kitty/kitty.conf

# 主题
include current-theme.conf

# 字体
font_size 13
font_family      family="Agave Nerd Font Mono"
bold_font        auto
italic_font      auto
bold_italic_font auto

# 行列
adjust_line_height 10
adjust_column_width 2

# 窗口
hide_window_decorations yes
background_opacity 0.8
initial_window_width  90c
initial_window_height 25c
window_padding_width   15
remember_window_size no

# 禁用所有退出确认
confirm_os_window_close 0

# 快捷键
map ctrl+q quit
```

### shell配置

#### nerd-font安装

```zsh
yay -S ttf-agave-nerd
```

#### zsh

```zsh
sudo pacman -S zsh # 安装

echo $SHELL # 查看当前shell
chsh -s $(which zsh)  # 修改默认 shell
```

#### oh-my-zsh

```zsh
sudo pacman -S oh-my-zsh-git # 安装
whereis oh-my-zsh # 找到oh-my-zsh文件夹
# /usr/share/oh-my-zsh
# 复制zshrc到~/.zhsrc

# 安装命令提示插件
cd /usr/share/oh-my-zsh/plugins
git clone git@github.com:zsh-users/zsh-autosuggestions.git
git clone git@github.com:zsh-users/zsh-syntax-highlighting.git

# 配置
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)

# 使得配置文件生效
source ~/.zshrc
```



