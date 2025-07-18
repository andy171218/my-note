Ventoy 是一款开源工具，可用于创建可启动的 USB 驱动器，支持直接从 ISO 文件启动而无需解压。

## windows上使用ventoy

### **1. 下载 Ventoy**

访问 ：[Releases · ventoy/Ventoy](https://github.com/ventoy/Ventoy/releases)

 下载最新版本：

- 选择 **Windows** 版本（如 ventoy-x.x.xx-windows.zip）。
- 解压下载的 ZIP 文件到任意文件夹。



### 2. 插入U盘

![img](.\assets\v2-011c13d124cd4d404d5d8b546ccdb84f_720w.png)



### 3. 将镜像导入

![img](.\assets\v2-72aed462372797670af498ad77be0bc5_720w.png)

剩下的空间可以放别的东西



## Linux上使用ventoy

在 linux上使用终端安装和配置 Ventoy 的完整指南：



### **Ventoy安装**

```
wget https://github.com/ventoy/Ventoy/releases/download/v1.0.96/ventoy-1.0.96-linux.tar.gz
tar -xvf ventoy-1.0.96-linux.tar.gz
cd ventoy-1.0.96
```



## **识别USB设别**

```
# 查看U盘（一般为sdb,请改为你的设备名）
sudo fdisk -l /dev/sdb

# 查看U盘格式
lsblk -f
```

*注意*： 确认您的 USB 设备标识（如 /dev/sdb），*操作将格式化整个设备！*



## **卸除挂载**

```
sudo umount /dev/sdb*
```



## **安全安装（禁用安全启动支持）**

```
sudo sh Ventoy2Disk.sh -i -s /dev/sdb
```

📌 重要选项：

- -i 强制安装（覆盖旧版）
- -r SIZE_MB 保留空间（如 -r 4096 保留 4GB）
- -s 启用安全启动支持



## **添加 ISO**

```
# 复制 ISO 文件 (替换实际路径)
sudo cp ~/路径/系统镜像.iso /mnt/ventoy/
```



## **启动验证**

重启电脑选择 USB 启动，Ventoy 将自动扫描并列出所有 ISO 文件



## **更新Ventoy（保留ISO文件）**

```
sudo sh Ventoy2Disk.sh -u /dev/sdb
```



## **问题**

**关闭安全模式（一般打不开都是这个问题）**

![img](.\assets\v2-cc4e3e3bc9144944cb219f325a22ef42_720w.gif)



**其他问题**

请参考：[**https://www.ventoy.net/cn/doc_news.html**](https://www.ventoy.net/cn/doc_news.html)