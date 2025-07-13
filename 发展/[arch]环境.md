
**环境安装**

```bash
sudo pacman -S nvm rustup uv

# rustup(默认工具链)
rustup default stable

# uv

# 安装python
uv pyhton list
uv python install 版本

# 临时运行文件
uv run -p 3.13 xx.py

# 安装依赖
uv pip install xxx

# nvm
echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.bashrc
source ~/.bashrc

# nvm的使用

# 安装最新版本
nvm install node

# 列出本地已安装版本
nvm ls

# 使用特定版本
nvm use 18.12.1

# 查看当前使用的 Node.js 版本
nvm current

# 查看node版本
node --version

# 查看npm版本
npm --version

# sdkman
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

#sdk的使用

# 查看所有 JDK 版本
sdk list java  
# 查看 Gradle 版本
sdk list gradle
# 安装
sdk install java 版本
# 切换版本
sdk use java 11.0.20-amzn
# 删除
sdk uninstall java 11.0.20-amzn
# 	查看当前使用的版本
sdk current


```

