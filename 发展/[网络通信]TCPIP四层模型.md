## 1. 应用层 (Application Layer)
**功能**：提供特定应用程序服务

**协议示例**：
- HTTP/HTTPS (网页)
- DNS (域名解析)
- SSH (安全登录)
- SMTP (邮件发送)
- FTP (文件传输)

**相关命令**：
```bash
# HTTP请求
curl -v https://example.com
wget https://example.com

# DNS查询
dig example.com
nslookup example.com

# 邮件测试
swaks --to user@example.com

# SSH连接
ssh username@host

# 端口测试(应用层)
nc -zv example.com 80
telnet example.com 80
```

## 2. 传输层 (Transport Layer)
**功能**：端到端通信，流量控制

**协议**：
- TCP (可靠传输)
- UDP (高效传输)

**相关命令**：
```bash
# 查看TCP/UDP连接
ss -tulnp       # 显示所有连接
ss -t -a        # 显示TCP连接
ss -u -a        # 显示UDP连接

# 端口扫描
nmap -sT example.com  # TCP扫描
nmap -sU example.com  # UDP扫描

# 网络测试
nc -l 8080            # 监听端口
nc example.com 80     # TCP连接测试

# 带宽测试
iperf3 -c server_ip   # 需要服务端
```

## 3. 网络层 (Internet Layer)
**功能**：寻址和路由

**协议**：
- IPv4/IPv6
- ICMP (ping)
- ARP (地址解析)

**相关命令**：
```bash
# IP地址配置
ip addr show          # 显示所有IP
ip addr add 192.168.1.100/24 dev eth0  # 添加IP

# 路由管理
ip route show         # 显示路由表
ip route add default via 192.168.1.1

# 网络测试
ping example.com
ping6 ipv6.example.com

# 路径追踪
traceroute example.com
tracepath example.com

# ARP缓存
ip neigh show         # 显示ARP表
arp -a
```

## 4. 网络接口层 (Network Interface Layer)
**功能**：物理传输

**技术**：
- Ethernet
- Wi-Fi
- PPP

**相关命令**：
```bash
# 接口信息
ip link show          # 显示所有接口
ethtool eth0          # 显示网卡详情

# 监控流量
sudo tcpdump -i eth0 -n 'tcp port 80'
sudo tshark -i eth0   # wireshark命令行版

# Wi-Fi管理
iw dev                # 显示无线设备
iwlist wlan0 scan     # 扫描WiFi

# 统计信息
ip -s link show eth0  # 接口统计
netstat -i            # 接口信息
```

## 完整数据流示例 (访问网站)

1. **应用层**：`curl https://example.com`
   - 生成HTTP请求
   - DNS解析(如果配置了本地缓存则跳过)

2. **传输层**：
   - 建立TCP三次握手 (`ss -t`可查看)
   - 分段HTTP数据

3. **网络层**：
   - 添加源/目的IP (`ip route get`可查路由)
   - 可能分片大数据包

4. **网络接口层**：
   - 封装为以太网帧 (`tcpdump`可抓取)
   - 通过网卡发送
