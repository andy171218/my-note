## **apt基本命令**



**更新并升级**

```
# 从配置的软件源下载最新的软件包列表,升级所有可升级的软件包
sudo apt update && sudo apt upgrade
# 完全升级系统
sudo apt full-upgrade
# 更激进的升级方式，会处理依赖关系变化
# 可能会删除一些软件包以解决依赖冲突
```



**安装新软件包**

```
sudo apt install <package_name>
# 示例：安装 nmap
sudo apt install nmap

# 安装特定版本的软件包
sudo apt install <package_name>=<version>
# 示例：安装特定版本的 python3
sudo apt install python3=3.9.2-3

# 查看软件报可用的版本
apt policy <package_name>
# 示例：查看 python3 可用版本
apt policy python3

# 阻止特定软件包被自动升级
sudo apt-mark hold <package_name>
# 示例：保持当前内核版本
sudo apt-mark hold linux-image-$(uname -r)

# 允许特定软件包被自动升级
sudo apt-mark unhold <package_name>
```



**卸载命令**

```
# 仅删除软件包（保留配置文件）
sudo apt remove 软件包名
# 彻底删除软件包（包括配置文件）
sudo apt remove --purge xxx
# 自动清理相关依赖
sudo apt autoremove
# 组合命令
sudo apt purge --auto-remove 软件包名

# 清理缓存
sudo apt clean
# 删除 /var/cache/apt/archives/ 中所有已下载的 .deb 包

sudo apt autoclean
# 只删除那些无法再从仓库下载的旧版本 .deb 包
```

ps:需要什么安装什么就可以了



**搜索软件包**

```
apt search <keyword>
# 在软件源中搜索包含关键字的软件包
# 示例：搜索与 wifi 相关的工具
apt search wifi
```



**显示软件包信息**

```
apt show <package_name>
# 显示软件包的详细信息
# 示例：查看 metasploit 的详细信息
apt show metasploit-framework
```



**列出已安装的软件包**

```
apt list --installed
# 列出所有已安装的软件包
# 可以配合 grep 进行过滤
apt list --installed | grep python
```



**修复损坏的依赖关系**

```
sudo apt --fix-broken install
# 尝试修复损坏的软件包依赖关系
```



**检查软件包依赖关系**

```
apt depends <package_name>
# 显示软件包的依赖关系
# 示例：查看 burpsuite 的依赖
apt depends burpsuite
```



**查看软件包反向依赖**

```
apt rdepends <package_name>
# 显示哪些软件包依赖指定的软件包
# 示例：查看 python3 的反向依赖
apt rdepends python3
```