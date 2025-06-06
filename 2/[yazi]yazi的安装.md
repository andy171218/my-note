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
```

## 5. 验证安装

```bash
which yazi
yazi --version
```
