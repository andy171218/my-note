## HTTP (超文本传输协议)

HTTP (HyperText Transfer Protocol) 是用于在网络上传输超文本的标准协议。

**特点：**
- 明文传输：所有数据都是未加密的
- 默认端口：80
- 无状态协议：每个请求独立，服务器不保留之前请求的信息
- 简单快速：通信速度快

**安全问题：**
- 信息窃听：第三方可以截获传输内容
- 信息篡改：传输内容可能被修改
- 身份伪装：无法验证通信双方的真实身份

## HTTPS (安全超文本传输协议)

HTTPS (HTTP Secure) 是 HTTP 的安全版本，通过 SSL/TLS 协议提供加密。

**特点：**
- 加密传输：所有数据都经过加密
- 默认端口：443
- 身份验证：通过证书验证网站身份
- 数据完整性：防止数据在传输中被篡改

**工作原理：**
1. 客户端发起 HTTPS 请求
2. 服务器返回包含公钥的数字证书
3. 客户端验证证书有效性
4. 双方协商生成会话密钥
5. 使用会话密钥加密通信内容

## 主要区别
| 特性        | HTTP       | HTTPS          |
|------------|------------|----------------|
| 安全性      | 不安全      | 安全            |
| 协议        | 应用层协议   | HTTP + SSL/TLS  |
| 端口        | 80         | 443            |
| 加密        | 无         | 有             |
| 证书        | 不需要      | 需要CA证书      |
| SEO        | 无优势      | 有排名优势      |

## 在Arch Linux上检查网站协议
你可以使用以下命令检查网站的协议：

```bash
# 使用curl检查
curl -I http://example.com
curl -I https://example.com

# 使用openssl检查HTTPS证书
openssl s_client -connect example.com:443 -servername example.com | openssl x509 -noout -dates
```

## SSL/TLS 详解

SSL (Secure Sockets Layer) 和 TLS (Transport Layer Security) 是用于在计算机网络中提供安全通信的加密协议。

### 发展历史
- **SSL 1.0**: 从未公开发布
- **SSL 2.0**: 1995年发布，已弃用(有严重漏洞)
- **SSL 3.0**: 1996年发布，现已弃用(POODLE攻击)
- **TLS 1.0**: 1999年发布(SSL 3.0的升级)
- **TLS 1.1**: 2006年发布
- **TLS 1.2**: 2008年发布
- **TLS 1.3**: 2018年发布(最新标准)

### 核心功能
1. **加密**：防止数据被窃听
2. **身份验证**：验证通信双方身份
3. **完整性**：确保数据未被篡改

### 工作原理

#### 握手过程(TLS 1.2为例)
1. **Client Hello**：客户端发送支持的加密算法列表和随机数
2. **Server Hello**：服务器选择加密算法并返回随机数
3. **证书验证**：服务器发送证书(包含公钥)
4. **密钥交换**：客户端生成预主密钥，用服务器公钥加密后发送
5. **会话密钥生成**：双方用随机数和预主密钥生成会话密钥
6. **加密通信**：使用会话密钥加密后续通信

#### TLS 1.3改进
- 简化握手过程(1-RTT或0-RTT)
- 移除不安全的加密算法
- 更安全的密钥交换机制

### 关键概念

#### 证书体系
- **CA (Certificate Authority)**：证书颁发机构(如Let's Encrypt, DigiCert)
- **证书链**：从根证书到终端证书的信任链
- **自签名证书**：未由CA签名的证书(仅适合测试)

#### 加密算法
- **对称加密**：AES, ChaCha20 (用于加密数据)
- **非对称加密**：RSA, ECC (用于密钥交换)
- **哈希算法**：SHA-256, SHA-384 (用于完整性校验)

### 在Arch Linux上的相关工具

#### 检查TLS信息
```bash
# 检查服务器支持的协议版本
openssl s_client -connect example.com:443 -tlsextdebug 2>&1 | grep "Protocol"

# 检查证书详细信息
openssl s_client -connect example.com:443 -showcerts | openssl x509 -noout -text

# 测试TLS 1.3支持(需要OpenSSL 1.1.1+)
openssl s_client -connect example.com:443 -tls1_3
```

#### 常用软件包
```bash
# OpenSSL (基础加密库)
sudo pacman -S openssl

# Let's Encrypt客户端
sudo pacman -S certbot

# 网络诊断工具
sudo pacman -S wireshark-qt tshark
```

