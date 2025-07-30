```zsh
#:#注释
# ~ 家目录
# . 当前目录
# .. 上级目录
# / 根目录

# 查看环境变量
env
# 查看某个变量
echo $XXX
# 设置环境变量
export LANG=zh_CN.UTF-8

# echo 双引号:解析并且换行
echo "$LANG
dquote> nihao"
zh_CN.UTF-8
nihao

# echo 单引号:不解析换行 
echo '$LANG
nihao'
$LANG
nihao

# \/
\ 转义
/ 路径

# ！历史命令调用，在find命令中是取反的意思。
!46 # 第46条历史命令

# * 通配符
ls *.txt

# $ 调用变量 小心使用
aaa=adny
echo $aaa
adny

# ; 分割指令 分别执行
ls ; cat 1.txt

# || 短路 前面的命令执行对了,后面的命令就不再执行了;前面错了,后面执行
ls || cat 1.txt

# && 前面对了,后面也执行;前面的错了,后面也不执行了
ls && cat 1.txt

# & 后台执行
top &

# `` 嵌套命令
mkdir `echo andy` # 先执行 echo andy 指令 然后再mkdir

# 文件名是破折号-
# 相对路径
cat ./-
# 重定向
cat < -
# 绝对路径
cat /home/bandit1/-

# 以 -开头的文件 -file.txt
touch -- -file.txt
cat -- -file.txt  # `--` 表示“选项结束”

# 有空格的文件
cat "spaces in name"  # 用引号包裹

# 文件名含特殊符号（如*、$）
cat "*.txt"  # 引号禁用通配符


```