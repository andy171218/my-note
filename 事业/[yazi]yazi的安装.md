# 完整安装 yazi 文件管理器指南

## 确保 Rust 环境正确配置

```bash
# 安装 Rust (如果尚未安装)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env

# 设置默认工具链
rustup default stable
rustup update
```

## 2. 安装构建依赖

```bash
sudo apt update
sudo apt install -y cargo pkg-config libssl-dev libxcb-shape0 libxcb-xfixes0
```

## 3. 安装 yazi

```bash
# 通过 cargo 安装
cargo install --locked yazi-fm

# 如果编译失败，尝试以下方法之一：

# 方法A：从源码构建
git clone https://github.com/sxyazi/yazi.git
cd yazi
cargo build --release
sudo cp target/release/yazi /usr/local/bin/

# 方法B：使用预编译二进制
wget https://github.com/sxyazi/yazi/releases/latest/download/yazi-x86_64-unknown-linux-gnu.tar.gz
tar -xvf yazi-*.tar.gz
chmod +x yazi
sudo mv yazi /usr/local/bin/

```

## 5. 验证安装

```bash
which yazi
yazi --version
```
