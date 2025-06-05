## kali的安装

kali的安装可以参考这个视频：
[kali的安装](https://www.bilibili.com/video/BV1Js4y1S7So/?spm_id_from=333.337.search-card.all.click)

## kali的配置

### 更换源，更新系统和软件

```bash
# 修改源
sudo nano /etc/apt/sources.list

# 把第一行注释掉
# 清华大学镜像站
# kali
deb https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main non-free contrib non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main non-free contrib non-free-firmware
# debian
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware
deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security bookworm-security main contrib non-free non-free-firmware

sudo apt update && sudo apt upgrade
```

### 语言与输入法

在 Kali Linux 英文环境下使用中文，可以通过以下步骤配置终端和系统支持中文显示及输入。

#### 更新系统并安装中文语言包

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install locales fonts-noto-cjk -y  # 包含中文字体和基础语言包
```

#### 生成中文区域配置

```bash
sudo dpkg-reconfigure locales
```

- 用方向键找到以下选项（按空格键选中）：

```bash
zh_CN.UTF-8 UTF-8
en_US.UTF-8 UTF-8
```

- 按回车确认，然后选择 `zh_CN.UTF-8` 作为默认区域（可选，若想保留英文界面则跳过）

#### 安装中文输入法（如Fcitx5）

```bash
sudo apt install fcitx5 fcitx5-pinyin fcitx5-configtool -y
```

- 配置环境变量

```bash
# 设置 Fcitx5 输入法环境变量（永久生效）
echo 'export GTK_IM_MODULE=fcitx5' >> ~/.zshrc
echo 'export QT_IM_MODULE=fcitx5' >> ~/.zshrc
echo 'export XMODIFIERS=@im=fcitx5' >> ~/.zshrc

# 重新加载 Zsh 配置
source ~/.zshrc
```

- 启动输入法（需图形环境支持）：

```bash
fcitx5 &
# 或者设为开机自启动（推荐）
mkdir -p ~/.config/autostart/
cp /usr/share/applications/org.fcitx.Fcitx5.desktop ~/.config/autostart/
```

通过 `fcitx5-configtool` 添加拼音输入法。

#### 验证中文显示

```bash
echo "测试中文显示" | iconv -f utf8 -t gb2312 | iconv -f gb2312 -t utf8
ls 中文目录名  # 若有中文文件/目录可测试显示
```

### 字体图标大小

**图标大小**
[图标大小](../pictures/2/icon-size.png)

**状态栏**
[状态栏](../pictures/2/bar-size.png)

**系统字体**
[系统字体](../pictures/2/sys-size.png)

**终端字体**
[终端字体](../pictures/2/ter-size.png)

**输入法字体**
[输入法字体](../pictures/2/shru-size.png)@ss

### 锁屏时间

[锁屏时间](../pictures/2/scrennlocktime.png)
