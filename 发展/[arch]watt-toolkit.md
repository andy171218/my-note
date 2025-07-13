
watt-toolkit是一款免费加速器,可以免费加速github,在windows上是安装了以后开箱即用,但是在linux上需要做一些配置才能够使用

### watt-toolkit的安装

```bash
yay -S watt-toolkit-bin-gitee
```

### watt-toolkit的配置

**证书导入**

证书在路径:/home/用户名/.local/share/Steam++/Plugins/Accelerator/

打开浏览器->设置->搜索:证书->查看证书->导入(信任)

**Host文件权限**

```bash
# 避免每次输密码
sudo chmod a+w /etc/hosts
# 若还是错误
sudo chmod a+r /etc/hosts

```

### 一些问题

这个工具主要是为了windows开发的,所以在linux上总是有一些小问题

遇到问题,比如说证书安装不上,导入了证书后还是无法加速,加速了但是没有速度...

这些情况,你可以尝试把证书删掉重装一次,把软件删掉重装一次,把系统重启一次
