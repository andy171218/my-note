```zsh
# 开启ssh
sudo systemctl enable --now sshd

# 允许root远程登录
sudo nano /etc/ssh/sshd_config

# 添加
PermitRootLogin yes

# 重启ssh服务
sudo systemctl restart sshd

# 使用ssh
ssh -p 2222 username@hostname 
```

