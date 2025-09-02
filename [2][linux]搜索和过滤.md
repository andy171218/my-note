### 管道

管道符号：`|`，可以将前面指令的执行结果，作为后面指令的操作内容。

例如:将ip a 中输出的内容作为tail命令的操作内容

```zsh
ip a | tail -4
# 输出
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:c2:15:4d:be:4e brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
```



### 搜索

```zsh
# 查找文件 (find)
find / -name "*.conf" 2>/dev/null  # 查找所有.conf文件
find . -user bandit7 -group bandit6 -size 33c
```





### 过滤

#### gerp

```zsh
# 按行模糊过滤
grep "xxx" xxx.txt
# -w:过滤完整单词 -n:显示行号
grep -w -n  "apple" xxx.txt
# 管道过滤
cat xxx.txt | grep "sss"
# 正则表达式
grep -P "(\d{1,3}\.){3}\d{1,3}" xxx.txt

# grep参数

-n 显示行号
[root@localhost ~]# grep -n'tcp'test.txt
# vitest.txt+48，表示进入vi的时候，光标直接定位的48行起始位置。

-c 对结果行计数
[root@localhost~]# grep -c‘tcp'test.txt
14

-i 不区分大小写
[root@localhost ~]# grep -n'tcp′ test.txt -i

-V 反向搜索，取反
[root@localhost~]#grep-n‘udp'test.txt-V#将不含有udp的行全部过滤出来

-w 精准匹配
[root@localhost ~]#grep -w'tcp'test.txt

-o 只显示匹配的结果，前面的第一个示例中我们用过-o参数
[root@localhost ~]# grep -o -n'tcp'test.txt

-A1 同时打印搜索结果行的后一行，A是after的简写
[root@localhost ~]# grep -A2'ftp'test.txt
[root@localhost~]# grep -A 2'ftp′test.txt

-B3 同时打印搜索结果行的前三行，B是before的简写
[root@localhost~]# grep -B2'ftp'test.txt

-C2 同时打印搜索结果行的上下各两行
[root@localhost~]# grep -C2'ftp'test.txt

-E 扩展正则表达式
#正则我们下面会细讲，先简单了解一下。
[root@localhost~]# grep -E.tp'test.txt#，就是正则表达式，表示任意的一个字符
[root@localhost~]#grep-E‘ftp|ssh'test.txt#查找ftp或者ssh，|是或者的意思，可以用多个ftp|ssh|telnet..

-P 使用per1正则广
#per1语言中设计的正则表达式写法规则，很强大，很多领域都支持per1正则的语法结构。
[root@localhost ~]# grep-P"d+"test.txt#匹配所有的数字
[root@localhost~]#grep -P"\d{4,}"test.txt#匹配4位的数字
```



#### sed

```zsh
# 按行修改替换
用法：sed[-nri][动作]目标文件文件
选项与参数：
-n：使用安静（silent）模式。在一般sed的用法中，所有来自STDIN的数据一般都会被列出到终端上。但如果加上-n参数后，则只有经过sed特殊处理的那一行（或者动作）才会被列出来。
-r：Sed的动作支持的是延伸型正则表示法的语法。（默认是基础正则表示法语法）
-i：直接修改读取的文件内容，而不是输出到终端。

动作说明：[ni[，n2]]function
nl，n2一般表示为行号，【，n2]表示这个参数可选，可有可无。

function:
a：指定行后面插入一行
d：删除
1：指定行前面插入一行
p：打印，#一般和前面的-n参数一起用
s：替换需要I忽略大小写，全局替换需要g

# 文本替换
# 将文件中的 "apple" 替换为 "orange"（只替换每行第一个）
sed 's/apple/orange/' file.txt

# 全局替换（所有匹配）
sed 's/apple/orange/g' file.txt

# 忽略大小写替换
sed 's/apple/orange/gi' file.txt

# 替换并直接修改原文件（加 `-i`）
sed -i 's/apple/orange/g' file.txt

# 文本删除
# 删除第 3 行
sed '3d' file.txt

# 删除包含 "error" 的行
sed '/error/d' file.txt

# 删除 10-20 行
sed '10,20d' file.txt

# 删除空行
sed '/^$/d' file.txt

# 插入/追加
# 在第 3 行前插入一行
sed '3i\插入的内容' file.txt

# 在第 3 行后追加一行
sed '3a\追加的内容' file.txt

# 在匹配行后追加
sed '/pattern/a\追加的内容' file.txt

# 打印特定行
# 打印第 5 行
sed -n '5p' file.txt

# 打印 10-15 行
sed -n '10,15p' file.txt

# 打印包含 "hello" 的行
sed -n '/hello/p' file.txt

# 打印文件最后一行
sed -n '$p' file.txt

# 多命令组合
# 替换并删除空行
sed -e 's/apple/orange/g' -e '/^$/d' file.txt

# 或用分号分隔
sed 's/apple/orange/g; /^$/d' file.txt

# 使用正则表达式
# 替换所有数字为 "X"
sed 's/[0-9]/X/g' file.txt

# 删除行首空格
sed 's/^[ \t]*//' file.txt

# 替换 "foo" 开头的行
sed 's/^foo/bar/' file.txt
```





#### awk

```zsh
# 按列过滤
# 基本语法
awk '模式 {动作}' 文件名

# 打印列
# 打印第1列和第3列
awk '{print $1, $3}' file.txt
# 打印最后一列
awk '{print $NF}' file.txt

# 指定分隔符
# 使用逗号分隔（默认是空格/制表符）
awk -F',' '{print $2}' data.csv
# 使用正则表达式作为分隔符（如冒号或空格）
awk -F'[: ]' '{print $1, $3}' file.txt


# NR 当前行号	
awk 'NR==3 {print}' file
# NF 当前行的列数	
awk '{print NF}' file
# FS 输入字段分隔符（默认空格）	
awk 'BEGIN{FS=":"} {...}'
# OFS 输出字段分隔符（默认空格）	
awk 'BEGIN{OFS=";"} {...}'
# FILENAME 当前文件名	
awk '{print FILENAME}'

# 条件过滤
# 打印第2列大于100的行
awk '$2 > 100 {print $0}' file.txt
# 打印包含 "error" 的行
awk '/error/ {print}' file.txt
# 打印第3列等于 "apple" 的行
awk '$3 == "apple" {print $1, $2}' file.txt

# 正则表达式
# 打印以 "A" 开头的行
awk '/^A/ {print}' file.txt
# 打印第2列匹配数字的行
awk '$2 ~ /[0-9]+/ {print}' file.txt

# 多文件处理
# 处理多个文件，并打印文件名
awk '{print FILENAME, $0}' file1.txt file2.txt
```



```zsh
# 统计
wc
# 统计多少行
wc -l xxx.txt
# 统计多少字
wc -c xxx.txt
# 统计多少个文件
ls /bin | wc -l

# --------------------

# 生成数字序列
seq 1 100
# 生成等宽数字序列
seq -w 1 100

# --------------------

# 排序(从小到大,从数字到字符)
cat xxx.txt | sort
# 排序(从小到大,从字符到数字)
cat xxx.txt | sort -n

# --------------------

# 去重(连续)要结合这sort使用
cat xxx.txt | sort | uniq
# c:字符出现了几次
cat xxx.txt | sort | uniq -c

# --------------------

# tr:字符替换、删除或压缩重复字符
# -c 或 --complement: 使用 SET1 的补集
# -d 或 --delete: 删除 SET1 中的字符，不进行转换
# -s 或 --squeeze-repeats: 将 SET1 中连续重复的字符压缩为单个字符
# -t 或 --truncate-set1: 将 SET1 截断为与 SET2 相同的长度

# 将小写字母转换为大写
echo "hello world" | tr 'a-z' 'A-Z'
# 输出: HELLO WORLD

# 将大写字母转换为小写
echo "HELLO" | tr 'A-Z' 'a-z'
# 输出: hello

# 删除所有数字
echo "abc123def456" | tr -d '0-9'
# 输出: abcdef

# 删除所有空格
echo "a b c d" | tr -d ' '
# 输出: abcd

# 将冒号替换为空格
echo "a:b:c:d" | tr ':' ' '
# 输出: a b c d

# 将多个字符替换为单个字符
echo "hello   world" | tr -s ' ' ' '
# 输出: hello world (压缩多个空格为一个)

# 删除文件中的非打印字符
cat file.txt | tr -d '\000-\011\013\014\016-\037'

# --------------------
# strings:用于从二进制文件中提取可打印字符串的实用工具
# 查看二进制文件中的可打印字符串
strings /bin/ls

# 查看特定进程的内存
strings /proc/[PID]/mem
```



