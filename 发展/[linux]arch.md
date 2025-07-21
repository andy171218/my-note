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
sudo nvim /etc/pacman.d/mirrorlist

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
sudo nvim /etc/pacman.conf

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

**blackarch**

```zsh
curl -O https://blackarch.org/strap.sh
chmod +x strap.sh
sudo ./strap.sh

sudo nvim /etc/pacman.conf

[blackarch]
Server = https://mirrors.aliyun.com/blackarch/$repo/os/$arch
```





### 环境



```zsh
sudo pacman -S nvm rustup uv

# rustup(默认工具链)
rustup default stable

# uv

# 安装python
uv pyhton list
uv python install 版本

# 临时运行文件
uv run -p 3.13 xx.py

# 安装依赖
uv pip install xxx

# nvm
echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.bashrc
source ~/.bashrc

# nvm的使用

# 安装最新版本
nvm install node

# 列出本地已安装版本
nvm ls

# 使用特定版本
nvm use 18.12.1

# 查看当前使用的 Node.js 版本
nvm current

# 查看node版本
node --version

# 查看npm版本
npm --version

# sdkman
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

#sdk的使用

# 查看所有 JDK 版本
sdk list java  
# 查看 Gradle 版本
sdk list gradle
# 安装
sdk install java 版本
# 切换版本
sdk use java 11.0.20-amzn
# 删除
sdk uninstall java 11.0.20-amzn
# 	查看当前使用的版本
sdk current
```



### 软件

```zsh
# 常用工具
yay -S archlinuxcn-keyring base base-devel blackarch-keyring docker docker-compose git neovim oh-my-zsh-git openssh yay zsh

# 开启ssh
sudo systemctl enable --now sshd

# 黑客工具
yay -S nmap aircrack-ng hydra

```



### 其他

#### 设置中文字体

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
```

#### 安裝输入法

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
