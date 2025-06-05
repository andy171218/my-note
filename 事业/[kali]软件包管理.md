## 星火商店(Spark Store)

**下载安装包**
官网下载地址:<https://gitee.com/spark-store-project/spark-store/releases>

**安装命令**

```bash
cd 安装包路径
sudo apt install ./spark-store_版本号_amd64.deb  # 替换为实际文件名
```

**启动方式**
开始菜单搜索:sparkstore

ps:常用的微信,百度网盘,包括ps都有

## apt安装

**安装命令**

```bash
# 直接输入想要的命令,如果没有安装会让你选择是否安装
python3
# 或者
sudo apt install xxx
```

**卸载命令**

```bash
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
