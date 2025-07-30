**创建文件**

```zsh
touch xxx.txt

# 批量创建文件(1.txt..10.txt)
touch {1..10}.txt
# 创建隐藏文件
touch .xx.txt
# 指定目录
touch /home/andy/xx.txt
```



**查看文件**

```zsh
ls

# 指定文件类型
ls *.txt
# 查看隐藏文件
ls -a
# 查看详细信息
ls -l
```



**查看文件类型**

```zsh
file 213.zip
```





**移动文件/文件夹**

```zsh
# 将xx.txt移动到/home/user目录下
mv xx.txt /home/user

# 重命名
mv xx.txt xxx.txt

# 重命名文件夹
mv xx xxx
```



**删除文件/文件夹**

```zsh
# 没有回收站
rm 4.txt 5.txt

# 强制删除
rm -f xx.txt
rm -f {5..10}.txt

# 删除文件夹
rm -r xxx

# 强制删除文件夹
rm -rf xxx
```



**复制文件**

```zsh
# 将1.txt复制到2.txt
cp 1.xtx 2.txt
# 递归复制目录
cp -r andy test
```



**查看当前目录**

```
pwd
```

**创建文件夹**

```zsh
mkdir xxx
# 创建多个文件夹
mkdir xxx{01..10}
# 依次创建
mkdir -p 1/2/3/4/5
```

**切换文件夹**

```zsh
cd /var/www/html  # 切换到绝对路径
cd ..  # 返回到上一级目录
cd ~  # 返回到用户主目录
```