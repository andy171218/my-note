### 安装
```bash
iwctl
station wlan0 connect xxx
输入密码
ping www.baidu.com

pacman -Sy archlinux-keyring
pacman -Sy archinstall
archinstall
```

### 换源

**换国内镜像源**

```bash
# 打开配置文件
sudo vim /etc/pacman.d/mirrorlist

#阿里源
Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
#中科大源
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
#清华源
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch

# 更新源
sudo pacman -Syyu

```

**添加非官方源**
```bash
# 打开配置文件
sudo vim /etc/pacman.conf

[archlinuxcn]
SigLevel = Optional TrustedOnly
# 阿里源
Server = https://mirrors.aliyun.com/archlinuxcn/$arch
#中科大源
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
#清华源
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

**导入 archlinuxcn key**

```bash
sudo pacman -Sy archlinuxcn-keyring
```

**安装yay  base-devel**

```bash
sudo pacman -Sy yay base-devel
```

### 设置中文字体

**字体安装**

```bash
sudo pacman -S noto-fonts-cjk
```

**系统设置**
```bash
sudo vim /etc/locale.gen
# 把以下内容前的#去掉
zh_CN.UTF-8 UTF-8

sudo locale-gen

# language:简体中文

```

### 安裝输入法

**安装**

```bash
sudo pacman -S fcitx5-im fcitx5-chinese-addons
# wayland 打开
```


**配置**

```bash
vim ~/.pam_environment

GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
```
