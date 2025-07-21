### 简介

cobalt strike(简称CS)是一款团队作战渗透测试神器,分为客户端及服务端,一个服务端可以对应
多个客户端,一个客户端可以连接多个服务端。

Cobalt Strike集成了端口转发、扫描多模式端口Listener、Windows exe程序生成、Windows dll动态
链接库生成、java程序生成、office宏代码生成,包括站点克隆获取浏览器的相关信息等。

### 目录结构

agscript  拓展应用的脚本
c2lint  用于检查profile的错误异常
teamserver  服务端程序
cobaltstrike, cobaltstrike.jar  客户端程序(java跨平台)
logs  目录记录与目标主机的相关信息
update, update.jar  用于更新CS
third-party  第三方工具







