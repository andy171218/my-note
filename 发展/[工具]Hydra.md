### 简介

Hydra是一款开源的暴力破解工具,支持FTP、MSSQL、MySQL、PoP3、SSH等暴力破解

### 参数介绍

hydra –l root –p root 172.26.2.36 ssh
-l 指定用户名
-L 指定用户名字典
-p 指定密码
-P 指定密码字典
-C 使用冒号分隔,比如root:root
-M 指定目标列表文件
-f 在找到第一对登录名或密码的时候停止

