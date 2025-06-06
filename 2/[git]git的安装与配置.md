```bash
# 安装git
sudo apt-get install git
# 配置git清华源，永久生生效
echo "export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'" >> ~/.zshrc

# 使更改立即生效
source ~/.zshrc

# 查看环境变量
echo $REPO_URL
```
