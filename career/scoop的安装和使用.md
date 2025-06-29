Scoop 是 Windows 上一个强大的命令行包管理器（类似 Linux 下的 apt 或 yum），专为开发者设计。让我为你详细介绍一下：

## 核心特点

1. **免安装**- 下载的软件都存放在用户目录下（默认 ~\scoop），不会污染系统目录
2. **便携式**- 所有应用都包含在独立目录中，容易清理和迁移
3. **开源**- GitHub 开源项目，社区维护
4. **无管理员权限**- 大部分操作不需要管理员权限

## scoop的安装

```shell
# 普通用户下，打开powershell
# 脚本执行策略更改，默认自动同意
Set-ExecutionPolicy RemoteSigned -scope CurrentUser -Force

# 执行安装命令（默认安装在用户目录下，如需更改请执行“自定义安装目录”命令）
iwr -useb scoop.201704.xyz | iex

# 更换scoop的repo地址
scoop config SCOOP_REPO "https://gitee.com/scoop-installer/scoop"
# 安装git
scoop install git
# 添加 bucket，默认拉取 sync 分支
scoop bucket add spc https://gitee.com/wlzwme/scoop-proxy-cn.git
# 只需要一个main一个spc大概就可以了

# 拉取新库地址
scoop update
```

## scoop的使用

```shell
# 软件管理

scoop install <app> 安装软件
scoop uninstall <app> 卸载软件
scoop update <app> 更新特定软件
scoop update * 更新所有已安装软件
scoop list 列出已安装软件
scoop search <app> 搜索软件
scoop info <app> 显示软件信息
scoop home <app> 打开软件主页

# 系统维护

scoop update 更新 Scoop 自身
scoop status 检查更新状态
scoop checkup 检查系统问题
scoop cleanup <app> 清理旧版本
scoop cleanup * 清理所有旧版本
scoop reset <app> 重置软件配置

# 例子：Git 错误

scoop install git
scoop reset git

# Bucket 管理

scoop bucket list 列出所有 buckets
scoop bucket add <name> [repo] 添加 bucket
scoop bucket rm <name> 删除 bucket
scoop bucket known 查看官方已知 buckets

# 常用 buckets

scoop bucket add main
scoop bucket add extras
scoop bucket add versions
scoop bucket add nirsoft

# 高级功能

scoop cache show 查看缓存
scoop cache rm <app> 删除缓存
scoop hold <app> 阻止软件更新
scoop unhold <app> 取消阻止更新
scoop export 导出安装列表
scoop import <file> 从列表安装

# 配置命令

scoop config 查看配置
scoop config <key> <value> 设置配置
scoop config rm <key> 删除配置

# 实用技巧

# 批量安装

scoop install git 7zip curl sudo

# 查看软件依赖

scoop depends <app>
```

### scoop-search

scoop-search是用来代替scoop search的工具，速度会快一点

```shell
# 使用 scoop-search(scoop搜索)
scoop install scoop-search
scoop-search git
```

## 一键安装脚本

```shell
<#
.SYNOPSIS
Scoop Installation Script (English Version)
.DESCRIPTION
Automated Scoop installation with Chinese mirror configuration
#>

# 0. Skip execution policy (already bypassed via command line)
Write-Host "Skipping execution policy configuration (bypassed via command line)" -ForegroundColor Yellow

# 1. Install Scoop (using Chinese mirror)
try {
    Write-Host "Installing Scoop..." -ForegroundColor Cyan
    Invoke-RestMethod -Uri "https://scoop.201704.xyz" -ErrorAction Stop | Invoke-Expression
    Write-Host "Scoop installed successfully" -ForegroundColor Green
    
    # Configure Chinese mirror
    scoop config SCOOP_REPO "https://gitee.com/scoop-installer/scoop"
}
catch {
    Write-Host "Scoop installation failed: $_" -ForegroundColor Red
    exit 1
}

# 2. Install Git first (required dependency)
try {
    Write-Host "Installing Git (required component)..." -ForegroundColor Cyan
    scoop install git
    Write-Host "Git installed successfully" -ForegroundColor Green
}
catch {
    Write-Host "Git installation failed: $_" -ForegroundColor Red
    exit 1
}

# 3. Add required buckets (after Git is installed)
$buckets = @{
    "main" = "https://github.com/ScoopInstaller/Main"
    "spc"  = "https://gitee.com/wlzwme/scoop-proxy-cn.git"
}

foreach ($bucket in $buckets.GetEnumerator()) {
    Write-Host "Adding $($bucket.Key) bucket..." -ForegroundColor Cyan
    scoop bucket add $bucket.Key $bucket.Value
}

# Update scoop after adding buckets
Write-Host "Updating Scoop repositories..." -ForegroundColor Cyan
scoop update
Write-Host "Scoop update completed" -ForegroundColor Green

# 4. Install all packages
$apps = @(
    "main/7zip",
    "main/fd",
    "main/fzf",
    "main/neovim",
    "main/lf",
    "main/oh-my-posh",
    "main/pwsh",
    "main/scoop-search",
    "spc/windows-terminal",
    "spc/hibit-uninstaller",
    "spc/watt-toolkit",
    "spc/neatreader",
    "spc/jpegview",
    "spc/openspeedy",
    "spc/pixpin",
    "spc/potplayer",
    "spc/baidudisk",
    "spc/Sandboxie-Classic",
    "spc/wechat",
    "spc/qbittorrent"
)

foreach ($app in $apps) {
    Write-Host "Installing $app..." -ForegroundColor Cyan
    scoop install $app
}

# 5. Completion message
Write-Host "`nAll packages installed successfully!" -ForegroundColor Green
Write-Host "Use 'scoop list' to view installed packages" -ForegroundColor Cyan
```

使用说明：
1. 将上面的代码保存为 scoop-full-init.ps1 文件
2. 右键powershell打开
