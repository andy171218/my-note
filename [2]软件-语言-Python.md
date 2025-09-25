## uv

### 安装运行

```zsh
# windows安装python
scoop install python

# windows安装uv
scoop install uv

# linux(arch)自带python
yay -s python

# linux(arch)安装uv
yay -S uv

# 安装python
uv pyhton list
uv python install 版本
uv python unnstall 版本

# 运行python
uv run python
uv run -p 3.13 python

# 临时运行文件
uv run -p 3.13 xx.py
```



### 依赖工具

```zsh
# 基本的main.py
# pyproject.toml
[project]
name = "proj"
version ="0.1.0"
dependencies=[]

# 添加依赖(安装到当前虚拟环境中)
uv add xxx
# 同步依赖
uv sync
# 删除依赖
uv remove xxx

# 运行
uv run main.py

# 安装工具(脱离当前工程,独立运行,整个系统可用)
uv tool install ruff
# 查看工具
uv tool list
```



### 打包

```zsh
# pyproject.toml
[project.scripts]
ai = "ai:main"

# 打包,whl文件(可以用uv add 或 uv tool install 安装)
uv build
```



## 注释

```python
# 单行注释 

"""
多行注释
"""

'''
多行注释
'''
```



## 变量

```python
# 变量是什么
数据变化:变量是计算机中用来存储数据的"容器"，它可以让计算机变得有记忆
变量在内存中划分一个区域,给它一个地址,在绑定一个变量名;通过寻址找到变量名就能得到那个值了
方便管理数据

# 语法
变量名=变量值

# =:赋值符号
#把一个数字10通过=符号绑定给变量名number
number= 10
#引用数据
print(number) # 10

# 变量名,命名规范(推荐用下划线,见名知意,先定义后引用,反复赋值会被覆盖)
变量名只能用字母，数字以及下划线三者组成
变量名不能以数字开头
变量名不能使用python关键字
变量名严格区分大小写
```



### 数值类型

#### int

```zsh
# int:整型
# 12 <class 'int'>
number =12
print(number , type(number))
```



#### float

```python
# float:浮点型
# 1.75 <class 'float'>
height = 1.75
print(height, type(height))
```



#### bool

```zsh
# bool:True(1),False(0)
# True <class 'bool'>
# 非0,非空,即为真
is_student = True
print(is_student, type(is_student))

print(bool(0))  # False
print(bool("0"))  # True
print(bool(""))  # False
print(bool([]))  # False
print(bool({"a": 1}))  # True

# True=1,False=0
print(True+False)
```



#### complex

```zsh
# complex:复数
# a是实部，b是虚部，a和b都是浮点数；
# z.real获得z的实部，
# z.imag获得z的虚部。
a=10.5
z = a + 15.5j
print(z)
print(z.rea1)
print(z.imag)
```



### 序列类型

#### str

```zsh
# 有索引
# str:字符串类型
# 双引号,或单引号包围
str1 = 'hello world'
str2 = "i love you"
str3 = '''
天上的星星参北斗
地下的月亮不说话
'''

# 索引取值
# 正向:0,1,2,3,4
# 负向:-1,-2,-3,-4
print(str1[0]) # h
print(str2[-3]) # y

# 切片取值:[开始索引(包含),结束下标(不包含),步长]
# 正向切片
msg = "helloword"
print(msg[0:4:1])  # he11
# 负向切片索引从-1开始
msg = "helloword"
print(msg[-5:-1])  # owor

# 字符串拼接 +
s1 = "ba"
s2 = "cd"
print(s1 + s2)
print(s1 + "hello")

# .join() 拼接,给定的list中的元素必须是str类型的
# 可以是列表、元组、字符串、字典、集合等
code_list = ["14", "dsc", "90"]
code = "-".join(code_list)
print(code) # 14-dsc-90

# len(str):计算长度,返回int
st = "hello"
print(len(st))  # 5

# 原生字符:不作为转义字符输出
raw_str = r"Hello\nworld"
print(raw_str)

# 查
# str.find(str)
# 作用：检测某个子字符串是否存在该字符串中，如果存在就返回该子字符的开始位置下标，否则返回是-1。
st = "hello world"
print(st.find("o"))  # 4
print(st.find("a"))  # -1不存在返回
print(st.find("o", 5))  # 从5的位置开始找,第二个o索引位置7

# str.index(str)
# 作用：检测某个子字符串是否存在该字符串中，女如果存在就返回该子字符的开始位置下标，否则报错
st = "hello world"
print(st.index("o"))  # 4
print(st.index("a"))  # 报错
print(st.index("o", 5))  # 从5的位置开始找,第二个o索引位置7

# str.count(str)
# 作用：计算某个子字符在字符串中出现的次数，没有出现返回0
st = "hello world"
print(st.count("o"))  # 2
print(st.count("a"))  # 0不存在返回

# 改
# str.split(分隔符号,分割次数)
# 作用：切分，指定分隔符号来切字符串；适合有规律的字符串；返回的数据是列表
# 默认是按照空格切分
file_name = "hello.py.yetgb.adf"
res_list = file_name.split(".", 2)  # 返回的是列表赋值给到一个变量
print(res_list)  # ['hello', 'py', 'yetgb.adf']

# str.replace(旧,新,次数)
# 作用：把字符串中的old（旧字符串）替换成new(新字符串)，如果指定第三个参数max，则替换不超过max次
str1 = "hello world"
str1 = str1.replace("l", "L", 2)  # 2代表替换两次，默认是全部替换
print(str1)  # heLLo world

# str.strip()
# 作用：移除字符串首尾指定的字符，默认去除换行和空格，也可以去除其他的字符
# 应用场景：用户在输入的时候，不小心在首尾输入了空格，有点难发现，在程序里增加一个方法，让用户输入数据后自动去除首尾的空格。
name = input("请输入名字：").strip()
if name == "phoebe":
    print("名字正确")
else:
    print("反之不正确")

# str.upper():转成大写
# str.lower():转成小写

# str.isdigit():判断字符串是否全为纯数字
print("125ab55".isdigit())  # False

# str.istitle():判断字符串里的单词是否首字母为大写，其他为小写字母
print("Hellolw2orld".istitle())  # False包含数字不行
print("Helloworld".istitle())  # True

# str.isspace():判断字符是为空格
print("5".isspace())  # False
print("".isspace())  # False
print(" ".isspace())  # True

# str.startswith(str)方法用于判断字符串是否以子字符串开头，如果是，返回True，否则返回False。
print("hello world".startswith("he"))  # True
print("helloworld".startswith("lo"))  # False

# str.endswith(str)方法用于判断字符串是否以子字符串结尾，如果是，返回True，否则返固False。
print("he1lo world".endswith("1d"))  # True
print("hello world".endswith("he"))  # False

# str.isalpha():方法用于判断字符串是否只包含字母，如果是，返回True，否则返回False。
print("hello world".isalpha())  # False
print("hello123".isalpha())  # False
print("hello".isalpha())  # True

# str.isalnum():判断字符串是否由字母和数字组成
print("hello world".isalnum())  # False
print("hello123".isalnum())  # True
print("hello".isalnum())  # True
print("hel1%**".isalnum())  # False
```



#### list

```zsh
# 有索引
# list:列表(可以增删改查)
# ['小帅', '小明', '小美', '大聪明', 14, True, ['c', 'a']] <class 'list'>
students_list =［'小帅','小明','小美','大聪明',14,True,['c','a']]
print(students_list, type(students_list))

# 空列表
li1=[]
li2=list()

# 访问列表中的值
# 索引：序列中的每个值都有对应的位置值，可以理解给每个值进行编号，称之为索引/下标。
lis=[123，'abc'，'456'，['hello"，‘world']]
#索引：0     1     2            3
#负向：-4   -3    -2           -1
#正向取值：
print(lis[0]) # 123
#负向取值
print(lis[-1]) # ['hello'，‘world']
#嵌套取值
print(lis[3][0]) # 'hello

# 切片取值:[开始索引(包含),结束下标(不包含),步长]
lie=['a','b','c','d','e','f','g']
print(lie[:]) # ['a', 'b', 'c', 'd', 'e', 'f', 'g']
print(lie[0:]) # ['a', 'b', 'c', 'd', 'e', 'f', 'g']
print(lie[2:5]) # ['c', 'd', 'e']
print(lie[::2]) # ['a', 'c', 'e', 'g']
print(lie[1:5:2]) # ['b', 'd']
print(lie[::-1]) # ['g', 'f', 'e', 'd', 'c', 'b', 'a']
print(lie[5:0:-2]) # ['f', 'd', 'b']

# 增
# list.append():整体添加，在列表末尾追加元素
li = [1, 2, 3]
li.append(4)
print(li) # [1, 2, 3, 4]

# list.extend(可叠加对象):分散添加，把可迭代对象拆开逐一添加
li.extend('abc') # [1, 2, 3, 'a', 'b', 'c']
li.append('abc') # [1, 2, 3, 'a', 'b', 'c', 'abc']

# list.insert(index，要插入的元素)
li = ["a", "b", "c"]
li.insert(2, "hello")
print(li)  # ['a', 'b', 'hello', 'c']

# 删
# list.remove():根据指定的元素值进行删除，如果删除的元素不存在会报错(默认是删除最开始出现的指定元素)
li = [1, 2, 23, 1, 2, 5, 4, 8, 7, 10, 545, 10, 415]
li.remove(10)
# li.remove('a')#删除不存在的值会引发error

# 删除偶数
li = [1, 2, 23, 1, 2, 5, 4, 8, 7, 10, 545, 10, 415]
copy_li = [1, 2, 23, 1, 2, 5, 4, 8, 7, 10, 545, 10, 415]
for i in copy_li:
    if i % 2 == 0:
        li.remove(i)
# 要触发移除，满足if语句
print(li)

# list.pop():根据索引删除元素，如果没有指定索引则默认删除最后一位
li = [1, 10, 545, 10, 415]
li.pop()
li.pop(3)
print(li) # [1, 10, 545]

# del列表[索引]：根据下标删除，注意删除的索引不存在会报错
li = ["a", "b", "c"]
del li[0]
print(li)  # ['b', 'c']

# 改
#列表名[下标]值
li = [1, 2, 3]
li[0] = 'abc'
print(li)

# title():首字母大写
li = ["apple", "jack", "andy"]
li[0] = li[0].title()
print(li) #['Apple', 'jack', 'andy']

# 查
# list.index():返回指定元素所在的位置下标，如果查找的元素不存在就报错
li = ["a", "b", "c"]
print(li.index("c"))
print(li.index("dd"))  # ValueError:'dd’isnotinlist值错误，查找的元素不在列表

# list.count():统计指定的元素在当前列表中出现的次数，如果查找的元素不存在就返回0
li = ["a", "b", "c"]
print(li.count("c"))  # 1
print(li.count("dd"))  # 0

# 排序
# list.sort():把列表按照特定的顺序排序，默认按照从小到大的顺序
li = [1, 2, 23, 1, 2, 5, 4, 8, 7, 10, 545, 10, 415]
li.sort(reverse=True) # 倒叙
print(li)

# list.reverse():把列表倒置过来，无顺序
li = [1, 2, 23, 1, 2, 5, 4, 8, 7, 10, 545, 10, 415]
li.reverse()  # [415, 10, 545, 10, 7, 8, 4, 5, 2, 1, 23, 2, 1]
print(li)

# min(li):最小值
# max(li):最大值

# 列表推导式:[表达式 for 临时变量 in 可迭代对象]
#创建一个整数列表
number_1ist = [number for number in range(1, 6)]
print(number_list)  # [1,2,3,4,5]

#例子
fruits = ["apple", "banana", "orange", "peach", "watermelon"]
# 把长度超过6的水果生成一个新的列表
new_fruits = []
for f in fruits:
    if len(f) >= 6:
        new_fruits.append(f)
print(new_fruits)
# 列表推导式
new_fruits = [f for f in fruits if len(f) >= 6]
print(new_fruits)

```



#### tuple

```zsh
# 有索引
# tuple:元组(不可变的列表:无法增删改查)
tu=（123，'abc'，'456'，['he11o'，'world'])

# 空元组
变量名=()
变量名=tuple()

# 注意
t1=("abc")
print(type(t1)) # <class'str'>
t2=("abc",)
print(type(t2)) # <class'tuple'>
```



### 散列类型

#### dict

```zsh
# 无索引
# dict:字典
# 每个用户的名字作为字典的key，Value值则是该用户的具体信息。
# 字典特性之一无序,是没有顺序的,可以存多个数据值,因此没有索引,此时想查找用户信息，只能通过key找value
# key是唯一的，但且只能是不可变类型的:str,int,tuple
# value值可以是任意类型，且可以一样
user_dict = {
    "小明": [18, "17658942580"],
    "小爱": [20, "15547859514"],
    "小帅": [19, "19958459871"],
    "大聪明": [18, "15647582552"],
}
print("age:", user_dict["小明"][0]) # age: 18
```



#### set

```zsh
# 无索引
# set:集合
# 用于存储无序且不重复的元素集合
元素不可变：集合本身是可变的，支持进行增加元素删除元素，但是存储的元素必须是不可变类型(布尔,数值,字符,元组)

# 注意：创建一个空集合必须用set()而不是{}，因为{}是用来创建一个空字典。
#使用set函数创建一个空集合
empty_set= set()
#使用花括号创建一个包含元素的集合
element_set={1,2,3,'a',5}
```



## 格式化输出

### 占位符

```zsh
# 输出的效果：我的名字是：小明，我的年龄是：18岁
# 连字符
name = "小明"
age = 18
print("我的名字是：" + name + "，我的年龄是：" + str(age) + "岁")

# 占位符
name = "小明"
age = 18
print("我的名字是：%s,我的年龄是：%d岁" % (name, age))

# '%s %d %f' % (str,int,float)
# %d:不保留小鼠,小数点后面的全部去掉,不会四舍五入
# %.2f:保留两位小数,%.4f:保留4为小数(会四舍五入)
# 占几个位置,就要传几个值
```



### f格式化

```zsh
# f'{变量} {变量}'
name = "小明"
age = 18
print(f"我的名字是{name}，我的年龄：{age}岁")

# 小数
num =3.141592653589793
print(f"num ={num:.2f}")
print(f"num ={num:.4f}")
#输出结果：
num =3.14
num =3.1416

# =
value="hello world"
print(f'{value=}')
#输出结果：value='helloworld'

# 计算
a = 10
b = 20
print(f"{a}+{b}={a+b}")
print(f"{a}-{b}={a-b}")
print(f"{a}*{b}={a*b}")
print(f"{a}/{b}={a/b}")
```



## 运算符

### 算数运算符

```zsh
加法:+ # 1+1=2
减法:- # 1-2=-1
乘法:* # 2*4=8
除法:/ # 4/2=2.0
整除:// # 10//3=3
取余:% # 10%3=1
幂次方:** # 2**10=1024
```



### 赋值运算符

```zsh
# 支持多变量同时赋值
a,b,c=1,2,'hello'
print(a)#输出1
print(b)#输出2
print(c)#输出‘hello"

# 支持多个变量赋相同的值
a=b=c=10
print(a,b,c)#10 10 10

# 交换值
x = 10
y = 99
x, y = y, x
print(f"{x=:.2f}, {y=:.4f}")  # x=99.56, y=10.2342
```



### 复合运算符

```zsh
age += 1  # age=age+1
age -= 3  # age=age-3
age *= 2  # age=age*2
age /= 4  # age=age/4
age //= 5  # age=age//5
age %= 6  # age=age%6
age **= 2  # age=age**2
```



### 比较运算符

```zsh
# 输出bool:true或false
# ==
print("a" == "a")  # True
print("1" == 1)  # False

# > < >= <=
num1 = 19
num2 = 15
print(numl > num2)  # True
print(num1 < num2)  # False
print(num1 >= num2)  # True
print(num1 <= num2)  # False

# ASCII编码127个字符
print("a" > "A")  # True
print(ord("a"))  # 97
print(ord("A")) # 65

# !=
a = 1
b = 2
print(a != b)  # True
print("1" != 1)  # True
```



### 逻辑运算符

```zsh
# x and y :逻辑"与"。如果x和y的值都为True，则返回最后后一个为True的值y；若x和y其中一个为False，则返回第一个为False的值
print(45 > 45 and 45 >= 23) # False

# x or y :逻辑"或"。如果x和y的值任意一个为True，则返回第一个为True的值。若x和y两个值都为Fasle，则返回最后一个为假的值
print('a'=='a'or'a'="b") # True

# not x :逻辑"非"。如果x的值为True，返回False；若x为False，返回True
not (100 > 50) # False

# 非0,非空都为真
print(2 and 55)  # 55(都为真,返回最后)
print("a" and "b" != "a")  # True
print(0 and "a")  # 0 (第一个为false,返回第一个)

print(2 or 55)  # 2
print("a" or "b" != "a")  # a
print(0 or "a")  # a
```



### 成员运算符

```python
# 成员运算符是用于判断一个元素是否存在于一个集合中的特殊运算符
# in
# list
li = ["a", "b", "c"]
print("a" in li)  # True
print("d" in li)  # False
# str
str1 = "hello world"
print("o" in str1)  # True
print("eo" in str1)  # False
# dic
dic = {"a": 1, "b": 2, "c": 5}
print("a" in dic)  # 字符a是不是字典的key值
print(2 in dic)  # False

# not in
name = input("请输入:")
name_list = ["phoebe", "小明"]
print(name in name_list)
```



### 身份运算符

```python
# 检查两个对象是否实际上即它们是否具有相同的内存地址
a =[1,2, 3]
b =[1, 2, 3]
c=a
print(id(a)) # 2403572474496
print(id(b)) # 2403572623552
print(a is b) # False
print(a is c) # True

# is和==的区别
==比较值是否相等,is比较地址是否一样

# 不可变类型,不会开辟新的地址
a=1
b=1
print(a is b)）#输出True
```



### 三目运算符

```zsh
# if:true,前面的返回;false,后面的返回
a=int(input("请输入a:"))
b=int(input("请输入b:"))
max_num =a if a>b else b
print(max_num)
```



## 条件语句

```zsh
# 示例:语法严格,冒号,缩进
num = 5
if num == 3:  # 判断num的值
    print("boss")
elif num == 2:
    print("user")
elif num == 1:
    print("worker")
elif num < 0:  # 值小于零时输出
    print("error")
else:
    print("roadman")  # 条件均不成立时输出
    
# 非0或非空都为真
char = "南"
if char:
    print("输出", char)
    
# if嵌套
# 分析：
# 1.输入数字
# 2.判断输入的数字是否在0-100的范围内
# 3.存在则再判断是否被3整除
num = int(input("请输入一个数字："))
if 0 <= num <= 100:
    if num % 3 == 0:
        print(f"{num}在0-100之间，并且能被3整除")
    else:
        print(f"{num}在0-100之间，但不能被3整除")
else:
    print(f"{num}不在0-100之间")
```



## 循环语句

### while循环

```python
# else 
count = 0
while count < 5:
   print count, " is  less than 5"
   count = count + 1
else:
   print count, " is not less than 5"
```



### for循环

```python
for letter in "Python":  # 第一个实例
    print("当前字母: %s" % letter)

fruits = ["banana", "apple", "mango"]
for fruit in fruits:  # 第二个实例
    print("当前水果: %s" % fruit)

# else
for num in range(10,20):  # 迭代 10 到 20 (不包含) 之间的数字
   for i in range(2,num): # 根据因子迭代
      if num%i == 0:      # 确定第一个因子
         j=num/i          # 计算第二个因子
         print ('%d 等于 %d * %d' % (num,i,j))
         break            # 跳出当前循环
   else:                  # 循环的 else 部分
      print ('%d 是一个质数' % num)
```



### 循环嵌套

```zsh
i = 2
while i < 100:
    j = 2
    while j <= (i / j):
        if not (i % j):
            break
        j = j + 1
    if j > i / j:
        print(i, " 是素数")
    i = i + 1
```



### 关键字

```zsh
# break 在语句块执行过程中终止循环，并且跳出整个循环
i = 1
while 1:            # 循环条件为1必定成立
    print(i)       # 输出1~10
    i += 1
    if i > 10:     # 当i大于10时跳出循环
        break

# continue 在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环
i = 1
while i < 10:   
    i += 1
    if i%2 > 0:     # 非双数时跳过输出
        continue
    print(i)         # 输出双数2、4、6、8、10
    
# pass 是空语句，是为了保持程序结构的完整性
# 输出 Python 的每个字母
for letter in 'Python':
   if letter == 'h':
      pass
      print '这是 pass 块'
   print '当前字母 :', letter
```





## 函数

### print()

```python
# python里最常见的一个内置函数，它是程序调试、结果展示等操作中的一个基础工具。
# 参数
values：输出的数据值，可以是多个值，值和值之间用逗号隔开,没用逗号默认是一个值,也可以不输出值
sep：分隔符，设置输出值和值之间的间隔符号，默认为空格间隔。
end：结束符，设置输出结束时的字符，默认为换行符

# values
print（'a'，'n'，'c'，'d'） # 输出四个字符
print('a''n''c''d')  # ancd输出一串字符
print()  # 空行

# sep
# 123---342---2342---2324
print(123,342,2342,2324,sep='---')

# end
# \n:换行符
print('我的名字是:',end='\n')
print('Andy')

# 类型
#输出字符串
print("Hello，world!")
#输出整数
print(123)
#输出浮点数
print(3.14)
#输出列表
print([1，2，3])
#输出字典
print({"name"："Alice"，"age"：30})
```



### input()

```python
# 语法
# 当程序执行到input函数时，会暂停执行，直到用户输入数据并按下回车键。这种行为使得程序能够根据用户的输入进行下一步的操作
# 需要将其赋值给变量
age = input("提示信息")

# 输入的数据都存储为str类型
value=input（"请输入任意数据："）
print（f"您输入的数据是{value}")
print（f"数据类型是{type（value)}")

'''
请输入任意数据：12
您输入的数据是12       
数据类型是<class 'str'>
'''

# 类型转换
number = float(input("请输入:"))

# BMI
weight = float(input("请输入体重kg："))
height = float(input("请输入身高m"))
bmi = weight / height**2
print(f"您的bmi值是：{bmi}")
if bmi < 18.5:
    print("体重过轻")
elif 18.5 <= bmi < 24:
    print("体重正常")
elif 24 <= bmi < 28:
    print("体重过重")
else:
    print("肥胖")
```

