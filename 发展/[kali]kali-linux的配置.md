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