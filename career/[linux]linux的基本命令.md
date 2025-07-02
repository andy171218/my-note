**文件和目录操作**

```
# 列出当前目录内容 (ls = list)
ls -la  # -l 长格式显示，-a 显示隐藏文件

# 切换目录 (cd = change directory)
cd /var/www/html  # 切换到绝对路径
cd ..  # 返回到上一级目录
cd ~  # 返回到用户主目录

# 显示当前工作目录 (pwd = print working directory)
pwd

# 创建目录 (mkdir = make directory)
mkdir -p ~/hacking/tools  # -p 创建多级目录

# 删除文件或目录 (rm = remove)
rm file.txt  # 删除文件
rm -rf directory/  # -r 递归删除，-f 强制删除(慎用！)

# 复制文件或目录 (cp = copy)
cp -r source/ destination/  # -r 递归复制目录

# 移动或重命名文件 (mv = move)
mv oldname.txt newname.txt  # 重命名
mv file.txt ~/Documents/  # 移动文件
```



**文件查看和编辑**

```
# 查看文件内容 (cat = concatenate)
cat /etc/passwd  # 显示整个文件内容

# 分页查看文件 (less)
less /var/log/auth.log  # 可上下翻页查看

# 查看文件开头 (head)
head -n 20 access.log  # 显示前20行

# 查看文件结尾 (tail)
tail -f /var/log/syslog  # -f 实时跟踪文件更新

# 使用nano简单编辑
nano file.txt

# 使用vim/nvim高级编辑
nvim /etc/hosts  # 使用neovim编辑文件
```



**系统信息**

```
# 显示系统信息 (uname = unix name)
uname -a  # -a 显示所有信息

# 显示磁盘使用情况 (df = disk free)
df -h  # -h 人类可读格式

# 显示目录/文件占用空间 (du = disk usage)
du -sh ~/Downloads/  # -s 总计，-h 人类可读

# 显示内存使用情况
free -h

# 显示系统运行时间和负载
uptime

# 显示进程信息 (ps = process status)
ps aux  # 显示所有进程
```



**网络相关**

```
# 检查网络连接 (ping)
ping google.com

# 显示网络接口信息 (ifconfig)
ip a  # 新版替代ifconfig的命令

# 显示网络连接 (netstat)
ss -tulnp  # 替代netstat的现代命令

# 下载文件 (wget)
wget https://example.com/file.zip

# 更强大的下载工具 (curl)
curl -O https://example.com/file.zip

# 追踪网络路由 (traceroute)
traceroute google.com
mtr google.com  # 更先进的替代品
```



**权限管理**

```
# 更改文件权限 (chmod = change mode)
chmod 755 script.sh  # 设置权限为rwxr-xr-x
chmod +x exploit.py  # 添加可执行权限

# 更改文件所有者 (chown = change owner)
sudo chown root:root /etc/shadow  # 修改所有者和组

# 切换用户 (su = substitute user)
su -  # 切换到root
su - username  # 切换到指定用户

# 以root权限执行命令 (sudo = superuser do)
sudo apt update  # 以root权限运行
```



**进程管理**

```
# 查找进程 (pgrep = process grep)
pgrep -l sshd  # 查找sshd进程

# 结束进程 (kill)
kill -9 1234  # 强制结束PID为1234的进程

# 动态查看进程 (top)
top
htop  # 更友好的替代品
```



**查找文件**

```
# 查找文件 (find)
find / -name "*.conf" 2>/dev/null  # 查找所有.conf文件

# 快速查找文件 (locate)
updatedb  # 先更新数据库
locate passwd  # 查找包含passwd的文件

# 在文件中搜索文本 (grep)
grep -r "password" /etc/  # 递归搜索
```



**压缩和解压**

```
# 解压tar.gz文件
tar -xzvf archive.tar.gz  # -x 解压，-z gzip，-v 详细，-f 文件

# 创建tar.gz压缩包
tar -czvf backup.tar.gz /path/to/dir/

# 解压zip文件
unzip file.zip

# 创建zip压缩包
zip -r archive.zip /path/to/dir/
```



**其他实用命令**

```
# 显示命令手册 (man = manual)
man ls

# 显示命令的简要说明 (whatis)
whatis grep

# 查找命令位置 (which)
which python

# 显示命令类型
type cd

# 命令历史 (history)
history | grep "apt install"  # 查找安装过的软件

# 清屏 (clear)
clear  # 或使用快捷键Ctrl+L
```