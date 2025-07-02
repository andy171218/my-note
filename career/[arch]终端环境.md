### terminal配置

**alacritty的安装**

```bash
sudo pacman -S alacritty
```

**alacritty的配置**

```bash
# ~/.config/alacritty/alacritty.toml

# ~/.config/alacritty/alacritty.toml

[window]
dimensions = { columns = 120, lines = 30 }
padding = { x = 5, y = 5 }
decorations = "none"
dynamic_title = true
opacity = 0.8  # 可选透明度

[font]
size = 12.0
normal = { family = "Agave Nerd Font Mono", style = "Regular" }
bold = { family = "Agave Nerd Font Mono", style = "Bold" }
italic = { family = "Agave Nerd Font Mono", style = "Italic" }
offset = { x = 1, y = 10 }  # 修正字体对齐

[scrolling]
history = 10000
multiplier = 3

#颜色主题可以在github上找想要的主题，复制他的配色.
[colors.primary]
background = "#1a1b26"
foreground = "#a9b1d6"

[colors.normal]
black = "#32344a"
red = "#f7768e"
green = "#9ece6a"
yellow = "#e0af68"
blue = "#7aa2f7"
magenta = "#ad8ee6"
cyan =  "#449dab"
white = "#787c99"

[colors.bright]
black = "#444b6a"
red = "#ff7a93"
green = "#b9f27c"
yellow = "#ff9e64"
blue =  "#7da6ff"
magenta = "#bb9af7"
cyan =  "#0db9d7"
white = "#acb0d0"

#光标
[cursor]
style = { shape = "Beam", blinking = "On" }

[env]
TERM = "xterm-256color"

```

### shell配置

**oh-my-bash的安装**

```bash
git clone https://github.com/ohmybash/oh-my-bash.git ~/.oh-my-bash
cp ~/.oh-my-bash/templates/bashrc.osh-template ~/.bashrc
source ~/.bashrc
```

**nerd-font安装**

```bash
yay -S ttf-agave-nerd
```

**.bashrc的配置**

1. 主题

```bash
# 列出主题列表
ls ~/.oh-my-bash/themes/

# 主题（默认是 "font"）
OSH_THEME="font"  # 其他主题如 "agnoster", "powerline"

```

2. 插件

```bash
ls ~/.oh-my-bash/plugins/       # 查看所有插件

# 插件列表（逗号分隔）
plugins=(git npm docker aws)
```

3. 别名

```bash
ls ~/.oh-my-bash/aliases/       # 查看所有别名模块

alias ll='ls -alF'
alias gs='git status'
```

4. 补全
```bash
ls ~/.oh-my-bash/completions/  # 查看所有补全
```

5. 配置生效

```bash
source ~/.bashrc
```

6. 删除

```bash
uninstall_oh_my_bash
```
