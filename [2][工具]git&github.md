**安装 Git**

```shell
scoop install git
```



**验证安装**

打开命令提示符（cmd）或 PowerShell，输入以下命令检查是否安装成功：

```shell
git --version
```



**配置 Git 用户信息** 

在首次使用 Git 前，需设置全局用户名和邮箱（与 GitHub 账户一致）：

```shell
git config --global user.name "YourGitHubUsername" 
git config --global user.email "your-email@example.com" 
git config --global core.sshCommand "ssh" 
git config --global http.schannelCheckRevoke false 
git config --global http.sslBackend "openssl" 
git config --global http.sslVerify false
```



**生成 SSH 密钥（推荐）** SSH 密钥用于安全连接 GitHub，无需每次输入密码。

**生成密钥**

在终端运行：

```shell
ssh-keygen -t ed25519 -C "your-email@example.com"
```

- 按回车使用默认路径（C:\Users\YourUser\.ssh\id_ed25519）。
- 可选设置密钥密码（直接回车跳过）。



**将公钥添加到 GitHub**

- 复制公钥内容（id_ed25519.pub）：

```shell
cat ~/.ssh/id_ed25519.pub
```

- 登录 GitHub → **Settings** → **SSH and GPG keys** → **New SSH key**，粘贴公钥。



**对于linux**

```zsh
chmod 600 ~/.ssh/id_ed25519 # 修改权限
```



**测试连接**

```shell
ssh -T git@github.com
```

看到 You've successfully authenticated 即表示成功。



**改用 HTTPS 端口（443）** GitHub 也支持通过 **443 端口** 的 SSH，适合被封锁的环境。 编辑 SSH 配置文件（~/.ssh/config），添加以下内容：

```shell
Host github.com     
Hostname ssh.github.com     
Port 443     
User git
```



**创造一个新的仓库**

```shell
echo "# my-note" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:andy171218/my-note.git
git push -u origin main
```



**将一个已有的仓库推送到远程仓库**

```shell
git remote add origin git@github.com:andy171218/my-note.git
git branch -M main
git push -u origin main
```

