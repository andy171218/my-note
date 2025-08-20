## 安装

### 在 wsl2 中安装

**打开 terminal**

```
# 安装kali-linux
wsl --install kali-linux --web-download
# 切换默认系统为kali-linux
wsl --set-default kali-linux
# 启动
wsl -d kali-linux
# 退出
exit
```



**换源**

```
# 修改源
sudo vim /etc/apt/sources.list

# 把第一行注释掉
#阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

sudo apt update && sudo apt upgrade
```



**安装 gui**

kex：https://www.kali.org/news/win-kex-version-2-0/ 

```
# wslg(kex:kali的GUI)
sudo apt install kali-win-kex
# 打开图形界面（经典模式）
kex --win -s
# 无缝界面
kex --sl --s
```



### 在 docker 中安装



**打开 terminal**

```
# 启动
docker run -it kalilinux/kali-rolling /bin/bash

# 更新
apt update

# 修改源
nvim /etc/apt/sources.list

# 把第一行注释掉
#阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

apt update && apt upgrade

# 需要什么装什么
apt install xxx

# 列出镜像(关注ID)
docker ps -a

# 启动镜像
docker start ID

# 回到镜像
docker attach ID

# 保存
docker commit ID 名称
```



**安装软件包**

以下是 **Kali Linux 主要工具包（Metapackages）对比表**，按你的需求整理（**无 GUI、命令行渗透测试**）：

| 工具包名称                       | 包含内容                                                     | 适合场景                       | 安装命令                                          |
| -------------------------------- | ------------------------------------------------------------ | ------------------------------ | ------------------------------------------------- |
| kali-linux-core                  | 最基础系统 + 少量核心工具（nmap, netcat, curl 等）            | 仅需基础环境，手动安装其他工具 | sudo apt install kali-linux-core                  |
| kali-linux-headless              | 所有无 GUI 渗透工具（metasploit, sqlmap, hydra, john, aircrack-ng 等） | 推荐！纯命令行渗透测试全覆盖   | sudo apt install kali-linux-headless              |
| kali-tools-top10                 | Kali 官方十大工具（nmap, metasploit, sqlmap, hydra 等）        | 快速获取核心工具               | sudo apt install kali-tools-top10                 |
| kali-tools-information-gathering | 信息收集工具（dnsenum, sublist3r, theHarvester 等）           | 专注侦察阶段                   | sudo apt install kali-tools-information-gathering |
| kali-tools-web                   | Web 渗透工具（burpsuite（CLI 模式）, sqlmap, nikto 等）         | Web 应用测试                    | sudo apt install kali-tools-web                   |
| kali-tools-passwords             | 密码攻击工具（hashcat, john, hydra 等）                       | 破解哈希/密码                  | sudo apt install kali-tools-passwords             |
| kali-tools-exploitation          | 漏洞利用工具（metasploit, exploitdb 等）                      | 漏洞利用阶段                   | sudo apt install kali-tools-exploitation          |



**附加说明**

1. **** **kali-linux-headless** **是最佳平衡选择**，涵盖大部分命令行工具且无 GUI 冗余。
2. **按需组合**：例如同时安装 kali-tools-web + kali-tools-passwords 可精准控制工具范围。
3. **Windows 用户建议**： 

- **WSL 2 Kali**：wsl --install -d kali-linux + 安装上表工具包。
- **Docker Kali**：轻量级容器化方案，适合单次任务。



**工具包依赖关系**

- 所有工具包均基于 kali-linux-core，安装时会自动包含基础依赖。
- 使用前务必更新： sudo apt update && sudo apt upgrade -y 



### 在虚拟机中安装

**安装 vmware 或其他虚拟机**

**安装镜像**

[Get Kali | Kali Linux](https://www.kali.org/get-kali/#kali-virtual-machines)




## 配置


### **更换源，更新系统和软件**

```
# 修改源
sudo vim /etc/apt/sources.list

# 把第一行注释掉
#阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

sudo apt update && sudo apt upgrade
```



### **语言与输入法**

在 Kali Linux 英文环境下使用中文，可以通过以下步骤配置终端和系统支持中文显示及输入。



### **更新系统并安装中文语言包**

```
sudo apt update && sudo apt upgrade -y
sudo apt install locales fonts-noto-cjk -y  # 包含中文字体和基础语言包
```



### **生成中文区域配置**

```
sudo dpkg-reconfigure locales
```

- 用方向键找到以下选项（按空格键选中）：

```
zh_CN.UTF-8 UTF-8
en_US.UTF-8 UTF-8
```

- 按回车确认，然后选择 zh_CN.UTF-8 作为默认区域（可选，若想保留英文界面则跳过）



### **安装中文输入法（如Fcitx5）**

```
sudo apt install fcitx5 fcitx5-pinyin fcitx5-configtool -y
```

- 配置环境变量

```
# 设置 Fcitx5 输入法环境变量（永久生效）
echo 'export GTK_IM_MODULE=fcitx5' >> ~/.zshrc
echo 'export QT_IM_MODULE=fcitx5' >> ~/.zshrc
echo 'export XMODIFIERS=@im=fcitx5' >> ~/.zshrc

# 重新加载 Zsh 配置
source ~/.zshrc
```

- 启动输入法（需图形环境支持）：

```
fcitx5 &
# 或者设为开机自启动（推荐）
mkdir -p ~/.config/autostart/
cp /usr/share/applications/org.fcitx.Fcitx5.desktop ~/.config/autostart/
```

通过 fcitx5-configtool 添加拼音输入法。



### **验证中文显示**

```
echo "测试中文显示" | iconv -f utf8 -t gb2312 | iconv -f gb2312 -t utf8
ls 中文目录名  # 若有中文文件/目录可测试显示
```



### **字体图标大小**

**图标大小**

![img](.\assets\v2-37375728d18a758eb30ed9dc3b452cbe_720w.png)



**状态栏** 

![img](.\assets\v2-94aaaa58b9feb4c512ff994c06b60b8e_720w.png)



**系统字体** 

![img](.\assets\v2-9e07133b42b555c55be43ced8bea07cf_720w.png)



**终端字体** 

![img](.\assets\v2-17cfbc97ed01c9ce5533a1817c6855e9_720w.png)



**输入法字体** 

![img](.\assets\v2-2df1bc4c31a9d66de1b16d4319fdbc9e_720w.png)



### **锁屏时间**

![img](.\assets\v2-35913b6fbd5ad794b763226b3c67697a_720w.png)