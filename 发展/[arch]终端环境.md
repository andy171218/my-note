### terminal配置

**kitty的安装**

```bash
sudo pacman -S kitty
```

**kitty的配置**

重载配置:`ctrl+shift+f5`
主题:`kitty +kitten themes`
字体:`kitty list-fonts --psnames`

```bash
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

```bash
yay -S ttf-agave-nerd
```

#### bash

**安装bash-completion**

```bash
sudo pacman -S bash-completion
```

**oh-my-bash的安装**

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

**oh-my-bash的配置**

1. 主题

```bash

# 查看有那些主题
ls $OSH/themes

# 设置主题 ~/.bashrc
OSH_THEME="agnoster"
```

2. 别名

```bash

# 查看别名
ls $OSH/aliases

# 设置别名
aliases=(
  general
)
# 常用别名
alias ll='ls -alF'
alias gs='git status'
alias gp='git push'
alias gcm='git commit -m'
alias ..='cd ..'
alias ...='cd ../..'
```

3. 插件

```bash

# 查看插件
ls $OSH/plugins

# 设置插件
plugins=(git python docker npm ssh)
```

**fzf**

`ctrl+r`:搜索历史
`ctrl+t`:搜索文件并输出
`alt+c`搜索目录并进入


4. 补全

```bash

# 查看补全
ls $OSH/completions/

# 设置补全
completions=(
  git
  composer
  ssh
)
```
