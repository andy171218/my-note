**初始化本地仓库**

```
# 在当前目录初始化一个新的Git仓库
git init
```



**配置用户信息（如果尚未配置）**

```
# 设置全局用户名
git config --global user.name "Your Name"

# 设置全局邮箱
git config --global user.email "your.email@example.com"
```



**添加文件到暂存区**

```
# 添加所有新文件和修改过的文件到暂存区
git add .

# 或者添加特定文件
# git add filename1 filename2
```



**提交更改**

```
# 提交暂存区的更改，并添加提交信息
git commit -m "Initial commit or your commit message"
```



**添加远程仓库**

```
# 添加远程仓库地址（将URL替换为你的实际仓库地址）
git remote add origin https://github.com/username/repository.git

# 或者使用SSH方式（推荐）
# git remote add origin git@github.com:username/repository.git
```



**推送到远程仓库**

```
# 首次推送时，使用-u参数设置上游分支
git push -u origin main

# 后续推送可以简化为
# git push
```



**如果遇到远程仓库不为空的情况**

```
# 先拉取远程更改（如果有）
git pull origin main

# 如果有冲突需要解决冲突后再提交
# 然后再次推送
git push origin main
```



**查看状态和日志**

```
# 查看当前仓库状态
git status

# 查看提交历史
git log

# 查看更简洁的提交历史
git log --oneline --graph
```



**分支操作**

```
# 创建新分支
git branch new-feature

# 切换分支
git checkout new-feature

# 创建并切换到新分支
git checkout -b new-feature

# 合并分支（先切换到主分支）
git checkout main
git merge new-feature
```



**其他常用命令**

```
# 查看远程仓库信息
git remote -v

# 从远程仓库获取最新更改但不合并
git fetch

# 丢弃工作区的修改
git checkout -- <file>

# 取消暂存的文件
git reset HEAD <file>
```