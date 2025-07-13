以下是 Git 连接 GitHub 的详细指南，适合新手快速上手：

---

### **1. 准备工作**
- **安装 Git**  
 
  ```bash
 sudo pacman -S git
 
 git --version
  ```

- **注册 GitHub 账号**  
  官网：https://github.com

---

### **2. 配置 Git 全局信息**

**设置用户名和邮箱（与 GitHub 一致）：**
```bash
git config --global user.name "YourName"
git config --global user.email "your@email.com"
```

**验证配置：**
```bash
git config --list
```

---

### **3. 生成 SSH 密钥（推荐）**
1. **生成密钥**（默认路径 `~/.ssh`）：
   ```bash
   ssh-keygen -t ed25519 -C "your@email.com"
   ```
   （提示时直接按回车使用默认设置）

2. **添加密钥到 SSH 代理**：
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

3. **将公钥添加到 GitHub**：
   - 复制公钥内容：
     ```bash
     cat ~/.ssh/id_ed25519.pub
     ```
   - 在 GitHub 设置 → **SSH and GPG keys** → 点击 **New SSH key**，粘贴并保存。

4. **测试连接**：
   ```bash
   ssh -T git@github.com
   ```
   看到 `You've successfully authenticated` 即成功。

---

### 使用git连接github

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
