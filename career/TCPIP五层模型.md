### **1. 物理层（Physical Layer）**

**功能**：负责在物理媒介（如网线、光纤、Wi-Fi）上传输原始比特流（0和1）。 **关键设备**：网卡（NIC）、集线器（Hub）、中继器（Repeater） **示例**：

- 以太网（Ethernet）
- Wi-Fi（IEEE 802.11）
- 光纤（Fiber Optic）

**Windows 相关命令**：

```
Get-NetAdapter  # 查看网络适配器信息
```



### **2. 数据链路层（Data Link Layer）**

**功能**：

- 将比特流组织成**帧（Frame）**
- 提供**MAC地址**（硬件地址）寻址
- 错误检测（如CRC校验）

**关键协议**：

- **以太网（Ethernet）**（局域网通信）
- **ARP（地址解析协议）**（IP → MAC 映射）
- **PPP（点对点协议）**（拨号上网）

**Windows 相关命令**：

```
arp -a  # 查看ARP缓存表（IP ↔ MAC 映射）
```



### **3. 网络层（Network Layer）**

**功能**：

- 负责**IP地址**寻址和**路由选择**（数据包如何从源到目的地）
- 处理不同网络之间的通信

**关键协议**：

- **IP（Internet Protocol）**（IPv4 / IPv6）
- **ICMP（Internet控制报文协议）**（如ping命令）
- **RIP / OSPF / BGP**（路由协议）

**Windows 相关命令**：

```
ping 8.8.8.8  # 测试网络连通性
tracert google.com  # 跟踪路由路径
```



### **4. 传输层（Transport Layer）**

**功能**：

- 提供**端到端**的可靠或不可靠数据传输
- 管理**端口号**（区分不同应用程序）

**关键协议**：

- **TCP（传输控制协议）**（可靠、面向连接，如HTTP、FTP）
- **UDP（用户数据报协议）**（不可靠、无连接，如DNS、视频流）

**Windows 相关命令**：

```
netstat -ano  # 查看当前网络连接和端口占用
Test-NetConnection -Port 80 google.com  # 测试TCP端口连通性
```



### **5. 应用层（Application Layer）**

**功能**：

- 直接面向用户，提供各种网络服务（如网页浏览、邮件收发）
- 数据格式由具体应用决定

**关键协议**：

- **HTTP / HTTPS**（网页浏览）
- **DNS**（域名解析）
- **FTP**（文件传输）
- **SMTP / POP3 / IMAP**（电子邮件）

**Windows 相关命令**：

```
nslookup google.com  # DNS查询
curl -v https://example.com  # 测试HTTP/HTTPS连接
```



### **总结对比（OSI vs. TCP/IP）**

| TCP/IP 五层 | OSI 七层                 | 主要功能       |
| ----------- | ------------------------ | -------------- |
| 应用层      | 应用层 + 表示层 + 会话层 | HTTP、FTP、DNS |
| 传输层      | 传输层                   | TCP、UDP       |
| 网络层      | 网络层                   | IP、ICMP       |
| 数据链路层  | 数据链路层               | 以太网、ARP    |
| 物理层      | 物理层                   | 网线、Wi-Fi    |



### **实际数据流动示例（访问网站）**

1. **应用层**：浏览器输入 https://google.com（HTTP/HTTPS）
2. **传输层**：TCP 建立连接（端口443）
3. **网络层**：IP 寻址（找到 Google 服务器）
4. **数据链路层**：封装成以太网帧（MAC 地址）
5. **物理层**：通过网线/Wi-Fi 传输比特流