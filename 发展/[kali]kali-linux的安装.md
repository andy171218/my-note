### 在实体机中安装

**ventoy烧录U盘**

[ventoyU盘烧录 ](./ventoyU盘烧录)

**图形化界面安装**



### 在wsl2中安装



**开启wsl2**

[wsl2的使用](./wsl2的使用)



**打开terminal**

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



**安装gui**

kex：https://www.kali.org/news/win-kex-version-2-0/ 

```
# wslg(kex:kali的GUI)
sudo apt install kali-win-kex
# 打开图形界面（经典模式）
kex --win -s
# 无缝界面
kex --sl --s
```



### 在docker中安装



**安装docker**

[docker在windows上的安装](./docker在windows上的安装)



**打开terminal**

```
# 安装并运行
docker run -it kalilinux/kali-rolling /bin/bash
```



**安装软件包**

以下是 **Kali Linux 主要工具包（Metapackages）对比表**，按你的需求整理（**无GUI、命令行渗透测试**）：

| 工具包名称                       | 包含内容                                                     | 适合场景                       | 安装命令                                          |
| -------------------------------- | ------------------------------------------------------------ | ------------------------------ | ------------------------------------------------- |
| kali-linux-core                  | 最基础系统 + 少量核心工具（nmap, netcat, curl等）            | 仅需基础环境，手动安装其他工具 | sudo apt install kali-linux-core                  |
| kali-linux-headless              | 所有无GUI渗透工具（metasploit, sqlmap, hydra, john, aircrack-ng等） | 推荐！纯命令行渗透测试全覆盖   | sudo apt install kali-linux-headless              |
| kali-tools-top10                 | Kali官方十大工具（nmap, metasploit, sqlmap, hydra等）        | 快速获取核心工具               | sudo apt install kali-tools-top10                 |
| kali-tools-information-gathering | 信息收集工具（dnsenum, sublist3r, theHarvester等）           | 专注侦察阶段                   | sudo apt install kali-tools-information-gathering |
| kali-tools-web                   | Web渗透工具（burpsuite（CLI模式）, sqlmap, nikto等）         | Web应用测试                    | sudo apt install kali-tools-web                   |
| kali-tools-passwords             | 密码攻击工具（hashcat, john, hydra等）                       | 破解哈希/密码                  | sudo apt install kali-tools-passwords             |
| kali-tools-exploitation          | 漏洞利用工具（metasploit, exploitdb等）                      | 漏洞利用阶段                   | sudo apt install kali-tools-exploitation          |



**附加说明**

1. ******kali-linux-headless** **是最佳平衡选择**，涵盖大部分命令行工具且无GUI冗余。
2. **按需组合**：例如同时安装 kali-tools-web + kali-tools-passwords 可精准控制工具范围。
3. **Windows用户建议**： 

- **WSL 2 Kali**：wsl --install -d kali-linux + 安装上表工具包。
- **Docker Kali**：轻量级容器化方案，适合单次任务。



**工具包依赖关系**

- 所有工具包均基于 kali-linux-core，安装时会自动包含基础依赖。
- 使用前务必更新： sudo apt update && sudo apt upgrade -y 



### 在虚拟机中安装

**安装vmware或其他虚拟机**

**安装镜像**

[Get Kali | Kali Linux](https://www.kali.org/get-kali/#kali-virtual-machines)

**开箱即用**

**其他kali设置**

[kali-linux的配置](./kali-linux的配置)