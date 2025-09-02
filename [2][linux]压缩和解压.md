```zsh
# 指定目录解压tar.gz文件
tar -xzf archive.tar.gz -C /home/andy/backup # -x 解压，-z gzip，-v 详细，-f 文件

# 创建tar.gz压缩包
tar -czf /home/jack/backup.tar.gz /home/andy/backup

# gzip压缩(不保留源文件)
gzip 1.txt

# gzip解压(不保留源文件)
gzip -d 1.txt.gz

# 解压zip文件
unzip file.zip

# 创建zip压缩包
zip -r backup.zip 1.txt 2.txt

# 压缩rar
rar a 压缩文件名.rar 文件或目录

# 解压rar
rar x 压缩文件.rar
```

