### 简介

Redis 是完全开源的,遵守 BSD 协议,是一个高性能的 key-value 数据库。

**应用场景**

- 存储 缓存用的数据
- 需要高速读/写的场合使用它快速读/写;

### 识别

默认端口:6379

**nmap**

```bash
nmap -v -Pn -p 6379 -sV --script="redis-info"

-v:显示过程
-Pn: no ping
-sV:版本探测
```

### 批量漏洞扫描


### 历史漏洞
