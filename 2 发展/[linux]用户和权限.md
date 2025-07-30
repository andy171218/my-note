## 用户和用户组

![image-20250724220904708](assets/image-20250724220904708.png)



## 用户管理

```zsh
# 创建一个用户
useradd test1
# 指定组创建用户
useradd test1 -g test1
# 删除一个用户,同时删除家目录的用户文件夹
userdel -r test1

# 设置密码
passwd test1

# 查看一个用户是否存在
id test1

# 查看用户状态
lchage -l test1

# 更改用户状态
usermod -L test1 # 禁用/锁定用户
usermod -U test1 # 解锁用户
usermod -g 组 用户 # 修改主组
usermod -G 组 用户 # 修改从属组

# /etc/passwd 存在哪些用户,多一个用户就多一行记录
# /etc/shadow 用户密码,加密

# 查看哪些用户连接
w

07:44:40 up 19 min,  1 user,  load average: 0.00, 0.00, 0.00
USER     TTY       LOGIN@   IDLE   JCPU   PCPU  WHAT
root     pts/1     07:25   19:13   0.11s  0.11s -zsh

# tty1:本地连接,pts/1:远程连接

# 切换用户 (su = substitute user)
su -  # 切换到root
su - username  # 切换到指定用户

```



## 用户组管理

```zsh
# /etc/group 查看有多少个用户组

# 添加组
groupadd test1

# 修改组
groupmod -n 新组名 旧组名 # 修改组名
```



## 权限管理

**文件权限**

```zsh
# 查看文件权限
ls -l /tmp/1.txt

-rw-r--r-- 1 root root 3.6K Jul 23 11:39 1.txt
# 第一段的第一个字符，表示文件类型-文件、d目录、1软链接（对应着windows快捷方式）、b块设备（ls/dev，可以看到硬盘sda等）
# 第一段第2-4字符，表示该文件所属用户的权限
# 第一段第5-7字符，表示该文件所属用户组的权限
# 第一段第8-10字符，表示其他用户对该文件的权限
# 第一个英文:用户 第二个英文:组
# 第11个字符是. 表示开启了selinux

r 4代表读权限read
w 2代表写权限write
x 1代表可执行权限executable
- 0空权限位，表示没有这个权限，9位权限不能少，没有的权限就用-代替。

权限值表
0 ---
1 --x
2 -w-
3 -wx
4 r--
5 r-x
6 rw-
7 rwx

ugo权限体系：
	rw-		r--  	r--
	user	group	other

# 更改文件权限 (chmod = change mode)
chmod 755 script.sh  # 设置权限为rwxr-xr-x
chmod +x exploit.py  # 添加可执行权限
chmod -x exploit.py  # 去掉可执行权限
chmod o-r 1.txt      # other去掉读权限
chmod g-x exploit.py # group去掉执行权限

# 更改文件所有者 (chown = change owner)
sudo chown root:root /etc/shadow  # 属主:属组

# 以root权限执行命令 (sudo = superuser do)
sudo apt update  # 以root权限运行

# 查看文件时间
stat 文件/文件夹
```



**目录权限**

```zsh
文件权限：rwx读写执行

目录的权限：rwx
r表示可以查看目录下有哪些文件
x表示可以cd切换到该目录
w表示可以在目录中创建、修改、删除文件等操作

为了安全操作：
文件权限默认：644权限、狠一点就给600权限
目录权限默认：755权限、狠一点就给700权限
```





## 可执行程序特殊目录(环境变量)

```zsh
# 查看环境变量
echo $PATH

# 将可执行文件添加到这些目录中,可以直接执行命令
```

