### 简介
Netdiscover是一种网络扫描工具，通过ARP扫描发现活动主机,可以通过主动和被动两种模式进行ARP扫描。通过主动发送ARP请求检查网络ARP流量，通过自动扫描模式扫描网络地,这种扫描的方式在内网中不容易被别人发现

```bash
sudo netdiscover -r 192.168.10.0/24
```
