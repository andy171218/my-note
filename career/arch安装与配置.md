## 安装
```bash
wlctl
station wlan0 connect xxx
输入密码
ping www.baidu.com

pacman -Syyu
archinstall
```

## 换源
在 `/etc/pacman.conf` 文件末尾添加以下两行：

```bash
[archlinuxcn]
Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
```

然后安装 GPG key
```bash
sudo pacman -Syu
sudo pacman -S archlinuxcn-keyring
```

## 配置aur

安装yay
```bash
sudo pacman -S yay
```

修改`aururl`

```bash
yay --aururl "https://aur.tuna.tsinghua.edu.cn" --save
```

## 语言
```bash
vim /eyc/locale.gen
# zh_CN UTF-8 UTF-8
sudo locale-gen
```

## 输入法

```bash
sudo pacman -S sudo pacman -S fcitx5 fcitx5-chinese-addons fcitx5-gtk fcitx5-qt fcitx5-configtool
sudo vim ~/.pam_environment
# 添加以下内容
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

## bash配置
oh-my-bash


## 更换terminal
st

## dwm


## neovim

