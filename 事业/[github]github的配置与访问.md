## 配置git clone源
```bash
git config --global url."https://gitclone.com/github.com/".insteadOf "https://github.com/"
```

## 命令行访问 GitHub 的完整指南

### 配置 Git

设置你的用户名和邮箱（这些信息会出现在你的提交记录中）：
```bash
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱@example.com"
```

查看配置：
```bash
git config --list
```

### 生成 SSH 密钥
SSH 密钥允许你安全地连接到 GitHub 而无需每次输入密码：
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
**将公钥添加到 GitHub：**
- 复制公钥内容：
```bash
cat ~/.ssh/id_ed25519.pub
```
- 登录 GitHub → Settings → SSH and GPG keys → New SSH key
- 粘贴你的公钥

测试 SSH 连接：
```bash
ssh -T git@github.com
```

### github基本工作流量
```bash
git clone git@github.com:用户名/仓库名.git
# 或使用 HTTPS
# git clone https://github.com/用户名/仓库名.git

# 查看状态
git status

# 添加更改
git add 文件名
# 或添加所有更改
git add .

# 提交更改
git commit -m "提交信息"

# 推送更改到远程仓库
git push origin 分支名

# 拉取远程更改
git pull origin 分支名
```
