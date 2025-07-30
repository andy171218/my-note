### 简介

Hydra是一款开源的暴力破解工具,支持FTP、MSSQL、MySQL、PoP3、SSH等几乎所有协议的暴力破解



**暴力破解**

指用枚举的方式来爆破用户信息。具体的流程是用事先收集好的数据集成一个字典,然后用字典不断进行枚举,直到枚举成功,密码能否破解的关键在于字典是否强大



**应用场景**

验证码
不含验证码后台
各种应用程序:phpmyadmin,tomcat,mysql
各种协议:ftp,ssh,rdp
爆破大马



**协议**

一台终端不管是连接一个网站还是连接另一个终端,一切数据传输都需要按照相应的协议(特定的数据加工格式),而连接不同的主机需要用到的协议是不一样的

比如说:访问网站(HTTP),另一台主机(SSH)



### 参数介绍

hydra –l root –p root 172.26.2.36 ssh
-l 指定用户名
-L 指定用户名字典
-p 指定密码
-P 指定密码字典
-C 使用冒号分隔,比如root:root
-M 指定目标列表文件
-f 在找到第一对登录名或密码的时候停止



### 使用

```zsh
# 查看帮助
hydra -h

# 使用代理:为了避免留下真实IP,采用代理服务器的方式
# 真实多台主机攻击一台主机,IP地址更换,需要加代理

# 参数介绍
-R 继续从上一次进度接着破解。
-S 指定爆破时使用SSL连接
-s PORT 可通过这个参数指定非默认端口。例如：某些http服务使用非80端口
-l LOGIN 指定破解的用户，对特定用户破解。root
-L FILE 指定用户名字典。参数值为存储用户名的文件的路径（建议为绝对路径）用户字典
-p PASS 小写，指定密码破解，用的少，一般是采用密码字典。
-P FILE 大写，指定密码字典。参数值为存贮密码的文件(通常称为字典)的路径（建议为绝对路径）密码字典
-e ns 可选选项，n：空密码试探，s：使用指定用户和密码试探。
-C FILE 使用冒号分割格式，例如“登录名：密码”来代替-L/-P参数。
-M FILE 指定目标列表文件一行一条。也就是指定多个攻击目标，此参数为存储攻击目标的文件的路径(建议为绝对路径)。注意：列表文件存储格式必须为"地址：端口"
-O FILE 指定结果输出文件。
-f 在使用-M参数以后，找到第一对登录名或者密码的时候中止破解。
-t TASKS 同时运行的线程数，默认为16。
-W TIME 设置最大超时的时间，单位秒，默认是30s。
-V／-V显示详细过程。
-4/-6:use IPv4 (default)/IPv6 addresses (put always in [] also in -M)
server 目标ip
service指定服务名，支持的服务和协议

# example
hydra -1 user -P passlist.txt ftp://192.168.0.1 #ftp默认端口号为21，如需指定端口，可以使用-s参数，或者在ip地址后面加：端口，比如ftp：//192.168.0.1:21

hydra -L userlist.txt -p defautpw imap://192.168.0.1/PLAIN
hydra -C defaults.txt -6 pop3s://[2001:db8::1]:143/TLS:DIGEST-MD5 #defau1ts.txt中每一行数据的格式为用户名：密码，DIGEST-MD5认证机制是基于MD5算法的LINUX安全机制认证，现在的意思就是说，密码暴破的时候，按照LINUX的MD5算法来进行密码暴破

hydra -l admin -p password ftp://[192.168.0.0/24]/
hydra -L logins.txt -P pws.txt -M targets.txt ssh

# 爆破数据库
hydra -L user.txt -P top100.txt -vV mysql://172.25.37.222
```





