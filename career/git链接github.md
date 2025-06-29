**1. 安装 Git**

```
scoop install git
```



**验证安装**

打开命令提示符（cmd）或 PowerShell，输入以下命令检查是否安装成功：

```
git --version
```



**2. 配置 Git 用户信息** 在首次使用 Git 前，需设置全局用户名和邮箱（与 GitHub 账户一致）：

```
git config --global user.name "YourGitHubUsername" 
git config --global user.email "your-email@example.com" 
git config --global core.sshCommand "ssh" 
git config --global http.schannelCheckRevoke false 
git config --global http.sslBackend "openssl" 
git config --global http.sslVerify false
```



**3. 生成 SSH 密钥（推荐）** SSH 密钥用于安全连接 GitHub，无需每次输入密码。

**生成密钥**

在终端运行：

```
ssh-keygen -t ed25519 -C "your-email@example.com"
```

- 按回车使用默认路径（C:\Users\YourUser\.ssh\id_ed25519）。
- 可选设置密钥密码（直接回车跳过）。



**将公钥添加到 GitHub**

- 复制公钥内容（id_ed25519.pub）：

```
cat ~/.ssh/id_ed25519.pub
```

- 登录 GitHub → **Settings** → **SSH and GPG keys** → **New SSH key**，粘贴公钥。



**测试连接**

```
ssh -T git@github.com
```

看到 You've successfully authenticated 即表示成功。



**改用 HTTPS 端口（443）** GitHub 也支持通过 **443 端口** 的 SSH，适合被封锁的环境。 编辑 SSH 配置文件（~/.ssh/config），添加以下内容：

```
Host github.com     
Hostname ssh.github.com     
Port 443     
User git
```