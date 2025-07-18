在 Windows 系统中使用 SSH 可以通过以下几种方式实现，具体取决于你的 Windows 版本和需求：

### **1. 使用内置的 OpenSSH 客户端（Windows 10/11 推荐）**

Windows 10（1809 版本后）和 Windows 11 已内置 OpenSSH 客户端，无需安装第三方工具。

### **步骤：**

 **启用 SSH 客户端**（如果未启用）： 

- 打开 **设置** → **应用** → **可选功能** → **添加功能**。
- 搜索并安装 **“OpenSSH 客户端”**。
- 或通过 PowerShell（管理员权限）运行： Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0 

 **连接到远程服务器**： 

- 打开 **命令提示符（CMD）** 或 **PowerShell**，输入： ssh username@远程服务器IP或域名 例如： ssh root@192.168.1.100 
- 首次连接时会提示确认主机指纹，输入 yes 继续。

**指定端口（默认22）**： ssh -p 2222 username@hostname 

**使用密钥登录（无密码）**： 

- 将公钥（id_rsa.pub）内容添加到服务器的 ~/.ssh/authorized_keys 文件。
- 使用 -i 指定私钥： ssh -i C:\path\to\private_key username@hostname 

### **2. 使用 Windows Terminal（可选）**

Windows Terminal 是一个现代化的终端工具，支持 SSH 连接：

1. 从 Microsoft Store 安装 **Windows Terminal**。
2. 直接在其中输入 ssh 命令，操作与上述相同。