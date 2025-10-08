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

# uv add 是添加包到项目依赖并安装（会更新配置文件）
uv add xxx
# 同步依赖
uv sync
# 删除依赖
uv remove xxx

# 运行
uv run main.py

# uv pip install 是仅安装包不记录到项目依赖
uv pip install requests
# 查看列表
uv pip list

# uv tool install 是专门安装可在终端直接运行的命令行工具
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



## 数据类型

| 数据类型       | 可变 / 不可变 | 可迭代 / 不可迭代 | 关键特性（视频重点）                                     |
| -------------- | ------------- | ----------------- | -------------------------------------------------------- |
| int/float/bool | 不可变        | 不可迭代          | 数值不可修改，无元素可遍历。                             |
| str            | 不可变        | 可迭代            | 字符序列，可遍历字符，不可修改单个字符。                 |
| tuple          | 不可变        | 可迭代            | 元素不可修改，但若含列表等可变元素，可修改该元素内部值。 |
| list           | 可变          | 可迭代            | 可自由增删改元素，遍历元素，地址不变。                   |
| dict           | 可变          | 可迭代            | 遍历键（默认）/ 值 / 键值对，可增删改键值对，地址不变。  |
| set            | 可变          | 可迭代            | 无序不重复，可增删元素，遍历元素，地址不变。             |



### 类型转换

```zsh
int(x) # 将x转换成一个整数类型数据
float(x) # 将x转换成一个浮点数类型数据
str(x) # 将x转换成一个字符串类型数据
eval(str) # 去除字符的引号，把中间部分当成python代码返回执行
list(s) # 将s转换成一个列表类型数据,要求是可叠加对象
tuple(s) # 将s转换成一个元祖类型数据,要求是可叠加对象
dict() # 可以把其他类型数据转化为字典类型,符合键值对
set(s) # 将s转换成一个集合类型数据
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

```python
# 有索引
# tuple:元组(不可变的列表:无法增删改查)
tu=(123，'abc'，'456'，['he11o'，'world'])

# 空元组
tu=()
tu=tuple()

# 注意
tu=(1) # int
tu=(1,) # tuple
t1=("abc")
print(type(t1)) # <class'str'>
t2=("abc",)
print(type(t2)) # <class'tuple'>

# 索引取值
fruits = ("apple", "banana", "cherry")
print(fruits[0])
print(fruits[-1])

# 切片取值
numbers = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
print(numbers[2:5])  # (2, 3, 4)

# 不可变性:无法增删改查
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

# 查
# dict[key]:通过key查value
user_dict = {
    "小明": [18, "17658942580"],
    "小爱": [20, "15547859514"],
    "小帅": [19, "19958459871"],
    "大聪明": [18, "15647582552"],
}
print("age:", user_dict["小明"][0]) # age: 18

# dict.get()
scores = {"张三": 100, "李四": 98, "王五": 45}
print(scores.get("李四"))  # 98
print(scores.get("小明"))  # None

# 改
# dict[key]=值
info_dict = {"张三": 100, "李四": 98, "王五": 45}
info_dict["张三"] = 88
print(info_dict)

# 增
# dict[key]=值(不存在的key就会新增)
info_dict = {"张三": 100, "李四": 98, "王五": 45}
info_dict["赵六"] = 88
print(info_dict)

# dict.update({})
info_dict = {"张三": 100, "李四": 98, "王五": 45}
info_dict.update({"小明":45,"小红":78})
print(info_dict)

# 删
# del dict[key]
info_dict = {"张三": 100, "李四": 98, "王五": 45}
del dict["张三"]
print(info_dict)

# dict.pop(key)
info_dict = {"张三": 100, "李四": 98, "王五": 45}
info_dict.pop({"张三"})
print(info_dict)

# dict.clear():清空列表

# for遍历字典
info_dict = {"张三": 100, "李四": 98, "王五": 45}
for key in info_dict:
    print(key, info_dict[key])
    
# dict.keys(),dict.values(),dict.items()
info_dict = {"张三": 100, "李四": 98, "王五": 45}
print(info_dict.keys())
print(info_dict.values())
print(info_dict.items())
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

# 增
# set.add()
s = {1, 2, 3}
s.add(4)

# set.update()
s.update([5, 6, 7])

# 删
# remove()
s.remove(3) 

# discard()
s.discard(10)  # 不会报错

# 集合的关系运算符
A = {1, 2, 3}
B = {1, 2, 3, 4, 5}

# 交集
print(A & B)  # {1, 2, 3}

# 并集
print(A | B)  # {1, 2, 3, 4, 5}

# 差集
print(B - A)  # {4, 5}
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

```python
加法:+ # 1+1=2
减法:- # 1-2=-1
乘法:* # 2*4=8
'''
对于数字类型，* 表示乘法运算（如 3 * 5 = 15）
对于字符串类型，* 表示重复操作，即将字符串重复指定的次数
'''
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
# break 在语句块执行过程中终止循环，并且跳出当前循环
# return可以跳出整个嵌套循环,因为结束掉的是整个函数
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

```python
# 作用
为了避免可维护性差、可读性差、增加错误风险等问题,就出现了函数
函数可以将一个功能代码封装到一个函数里,用的时候直接调用函数就能实现该功能

'''
函数代码块以def关键词开头，后接函数名称和小括号()
小括号之间可以用于定义参数，任何传入参数和自变量必须放在小括号中间
函数的第一行语句可以选择性地使用文档字符串存放函数说明
函数内容以冒号起始，再缩进。
return表示结束函数，且把后面的值返回给调用方。没写return的相当于返回None
'''

# 定义函数
def 函数名():
    函数代码

# 调用函数
函数名()

# 无参无返回值
def func():
	print("输出")
    
# 有参无返回值
def func(x, y):
    z = x + y

# 无参有返回值
def func():
    x = 1
    return x + 1

# 有参有返回值
def func(x, y):
    return x + y

# 空函数(pass占位)
def func():
    pass

# 单独的函数名:函数的内存地址
```



### 参数

```python
# 函数体内的参数只能在函数内部使用
# 位置参数:位置和数量是多少就传多少
def func(name, greeting):
    print(name+greeting)

func("小明","你好")

# 关键字参数
def func(name, greeting):
    print(name+greeting)

func(greeting="你好",name="小明")

# 默认参数:默认参数只能在位置参数后面,否则会报错(放在最后)
def func(name, greeting="你好"):
    print(name+greeting)
# 新传入的会覆盖默认的
func("小明","hello")

# 可变参数:传入实参不固定
# 可变位置参数
def func(*args):
    print(args, type(args))

func(1, 2, 3, 4, 5, 6) # (1, 2, 3, 4, 5, 6) <class 'tuple'>
func("a", "b", "c") # ('a', 'b', 'c') <class 'tuple'>
# 例子
def func(*args):
    total = 0
    for number in args:
        total += number
    print(total)

func(12, 3, 4, 5, 8)
func(12, 3, 8)
func(12, 3)

# 可变关键字参数
def func(**kwargs):
    print(kwargs)
    for k, v in kwargs.items():
        print(f"{k} = {v}")

func(name="Alice", age=30, city="New York")
func(country="USA", profession="Engineer")

'''
结果:
{'name': 'Alice', 'age': 30, 'city': 'New York'}
name = Alice
age = 30
city = New York
{'country': 'USA', 'profession': 'Engineer'}
country = USA
profession = Engineer
'''
```



### 返回值

```python
# 在程序开发中，有时候会希望一个函数执行程序结束后，告诉调用者一个结果，以便调用者针对具体的结果做后续的处理。
def login():
    username = input("请输入账号名：")
    password = input("请输入密码：")
    if username == "admin" and password == "123456":
        return True
    else:
        return False


def shop_car():
    print("查看购物车...")


print("请先登录")
result = login()
if result:
    shop_car()
else:
    print("请重新登录")

# 返回值可以返回任何类型,一个函数有无返回值,取决于调用者需不需要返回值
# return后的代码不会被执行,因为return是结束掉了函数
```



### 类型提示

```python
# 希望a是int，b是str，返回值是str
# 只是一个类型提示,实际上什么类型都可以

def func(a: int, b: str) -> str:
    print("a = ", a)
    print("b = ", b)
    return "c"

func(1, "2")
```



### 作用域

| 分类维度               | 具体类别 / 操作              | 核心说明                                                     | 示例 / 注意事项                                              |
| ---------------------- | ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **一、作用域分类**     | 内置作用域                   | Python 解释器启动时自动加载内置模块（如`print()`、`len()`），提供基础功能支持 | 无需手动导入，直接使用`print("Hello")`即可调用内置作用域的函数 |
|                        | 全局作用域                   | 对应单个`.py`文件内部，文件执行时产生的数据存储于此，作用范围覆盖整个文件 | 在`.py`文件顶部定义`x = 15`，该变量为全局变量，文件内所有函数均可访问 |
|                        | 局部作用域                   | 函数内部的独立空间，函数调用时创建，存储函数内定义的数据，函数执行完毕后销毁 | 函数`def func(): y = 20`中，`y`为局部变量，仅在`func()`内部生效 |
|                        | 嵌套作用域                   | 函数嵌套场景下，外层函数包含内层函数的空间范围，内层函数可访问外层函数的局部数据（需满足查找规则） | 外层函数`def outer(): a = 5; def inner(): print(a)`，`inner()`所处的外层函数空间即为嵌套作用域 |
| **二、作用域关键顺序** | 加载顺序                     | 内置作用域 → 全局作用域 → 局部作用域（遵循 “解释器启动→执行文件→调用函数” 的流程） | 运行`.py`文件时，先加载`print`等内置函数，再读取文件内全局变量，最后执行函数时创建局部空间 |
|                        | 查找顺序（局部空间发起）     | 局部 → 全局 → 内置（优先从当前所在局部空间查找，未找到则向上层查找） | 局部有`x=10`、全局有`x=55`，在局部访问`x`时，结果为 10       |
|                        | 查找顺序（全局空间发起）     | 全局 → 内置（不回溯局部空间，仅在全局和内置范围查找）        | 局部有`x=10`、全局有`x=55`，在全局访问`x`时，结果为 55       |
|                        | 存活顺序                     | 内置名称空间（随解释器启停）→ 全局名称空间（随文件执行完毕销毁）→ 局部名称空间（随函数调用结束销毁） | 解释器关闭后，`print`等内置函数失效；文件执行完，全局变量`x=15`销毁；函数调用结束，局部变量`y=20`释放 |
| **三、变量类型**       | 全局变量                     | 函数外部定义，作用范围覆盖整个文件及所有函数，程序执行完毕后回收；尽量少用，优先通过函数参数 / 返回值传递数据 | 全局变量`x=15`，函数`func1()`和`func2()`均可访问；长期占用内存，避免过多定义 |
|                        | 局部变量                     | 函数内部定义（形参也属此类），仅在函数内生效，函数执行完毕后销毁；不同函数可同名，互不影响，用于临时存储数据 | 函数`func1(): y=20`和`func2(): y=30`，两个`y`互不干扰，仅在各自函数内使用 |
| **四、变量修改方法**   | 修改全局可变类型（如列表）   | 无需特殊关键字，直接操作或作为参数传递修改，因可变类型传递内存地址，修改会同步影响全局 | 全局`list1 = [1,2]`，函数内`list1.append(3)`，全局`list1`最终为`[1,2,3]` |
|                        | 修改全局不可变类型（如 int） | 需用`global`关键字声明变量为全局变量，再赋值修改；必须调用函数使修改代码生效 | 全局`x=10`，函数内`global x; x=20`，调用函数后全局`x`变为 20；不声明`global`则仅修改局部变量 |
|                        | 嵌套函数修改外层变量         | 需用`nonlocal`关键字声明变量为外层函数的局部变量，再修改；仅在嵌套函数内生效，且外层函数需先定义该变量 | 外层`def outer(): a=5; def inner(): nonlocal a; a=10`，调用`outer()`后，外层`a`变为 10；外层无`a`时用`nonlocal`会报错 |
| **五、关键字区别**     | `global`关键字               | 作用：函数内声明变量为全局变量；适用场景：多个函数操作同一全局变量；特殊情况：全局无该变量时，声明后定义会成为全局变量 | 函数`func1(): global x; x=15`和`func2(): global x; x=20`，调用后全局`x`最终为 20；全局无`x`时，`func1()`执行后`x`成为全局变量 |
|                        | `nonlocal`关键字             | 作用：嵌套函数内声明变量为外层函数局部变量；适用场景：嵌套函数共享 / 修改外层局部变量；限制：无法作用于全局变量，依赖外层函数先定义变量 | 仅能在`outer()`的内层`inner()`中使用；外层无`a`时，`inner()`内`nonlocal a`会直接报错，且无法引用全局`a` |



### 内置函数

#### print()

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



#### input()

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



#### zip()

```python
# 将多个序列按位置配对
names = ["Alice", "Bob"]
ages = [25, 30]
for name, age in zip(names, ages):
    print(name, age)
# 输出:
# Alice 25
# Bob 30
```



#### enumerate()

```python
fruits = ["apple", "banana", "cherry"]
for index, value in enumerate(fruits):
    print(index, value)
# 输出:
# 0 apple
# 1 banana
# 2 cherry
```



#### sorted()

```python
# 对序列进行排序
print(sorted([3, 1, 4, 2]))  # 输出: [1, 2, 3, 4]
print(sorted("python"))      # 输出: ['h', 'n', 'o', 'p', 't', 'y']
```



#### range()

```python
# 生成一个整数序列
for i in range(5):
    print(i)  # 输出: 0, 1, 2, 3, 4

for i in range(2, 8):
    print(i)  # 输出: 2, 3, 4, 5, 6, 7
```



#### map()

```python

```



## 模块

```python
# 模块是组织与复用代码的重要工具。
# 模块可将代码组织起来,一个.py文件
```



### 内置模块

```zsh
# Python 自带，无需额外下载即可使用
```



#### time

```python
# 功能：获取当前时间、时间格式转换、程序延时等
import time  # 导入内置time模块

# 1. 获取当前时间戳（从1970年1月1日至今的秒数）
timestamp = time.time()
print("当前时间戳：", timestamp)  # 输出示例：1728000000.123456

# 2. 将时间戳转换为本地时间（结构化时间对象）
local_time = time.localtime(timestamp)
# 3. 格式化结构化时间为字符串
formatted_time = time.strftime("%Y-%m-%d %H:%M:%S", local_time)
print("当前本地时间：", formatted_time)  # 输出示例：2024-09-03 14:20:00

# 4. 程序延时1秒
print("开始延时...")
time.sleep(1)
print("延时结束！")
```



#### random

```python
# 功能：生成随机整数、随机浮点数、随机选择元素等，常用于抽奖、随机排序场景。
import random  # 导入内置random模块

# 1. 生成1-100（包含边界）的随机整数
random_int = random.randint(1, 100)
print("1-100的随机整数：", random_int)  # 输出示例：47

# 2. 从列表中随机选择1个元素（如抽奖场景）
fruits = ["苹果", "香蕉", "橙子", "草莓"]
random_fruit = random.choice(fruits)
print("随机选中的水果：", random_fruit)  # 输出示例：香蕉

# 3. 打乱列表顺序（如洗牌场景）
random.shuffle(fruits)
print("打乱后的列表：", fruits)  # 输出示例：["草莓", "苹果", "橙子", "香蕉"]
```



#### os

```python
# 功能：操作文件 / 文件夹（创建、删除、查看路径）、获取环境变量等，常用于文件管理场景。
import os  # 导入内置os模块

# 1. 获取当前工作目录（程序运行的当前路径）
current_dir = os.getcwd()
print("当前工作目录：", current_dir)  # 输出示例：C:\Users\Username\Desktop

# 2. 创建新文件夹（若不存在则创建）
new_folder = "test_folder"
if not os.path.exists(new_folder):
    os.mkdir(new_folder)  # 创建文件夹
    print(f"已创建文件夹：{new_folder}")
else:
    print(f"文件夹 {new_folder} 已存在")

# 3. 判断文件是否存在（如检查配置文件是否存在）
file_path = "config.txt"
if os.path.exists(file_path):
    print(f"文件 {file_path} 存在")
else:
    print(f"文件 {file_path} 不存在")
```



#### math

```python
# 数学运算
import math

print(math.pi)        # 圆周率 π
print(math.sqrt(25))  # 平方根，输出: 5.0
print(math.sin(math.pi/2))  # 正弦值，输出: 1.0
print(math.ceil(4.2))  # 向上取整，输出: 5
```



#### re

```python
'''
re.findall()
'''

# 从文本中提取所有手机号（国内手机号规则：1 开头，第二位 3-9，后续 9 位数字）
import re

text = "我的手机号是13800138000，朋友的是15912345678，无效号码是23800138000"
pattern = r"1[3-9]\d{9}"  # 手机号正则：1 + 3-9 + 9位数字
result = re.findall(pattern, text)
print(result)  # 输出：['13800138000', '15912345678']

'''
re.search ()
'''

# 在整个字符串中搜索第一个匹配项，不限制从开头开始。示例：从一段文本中提取第一个电话号码
import re

text = "联系电话：13812345678，备用电话：13987654321"
pattern = r"1[3-9]\d{9}"  # 手机号正则：1开头，第二位3-9，后接8位数字

result = re.search(pattern, text)
if result:
    print("找到的第一个手机号：", result.group())  # 输出：13812345678

'''
re.match ()
'''

# 仅从字符串开头匹配，若开头不匹配则返回None。示例：验证字符串是否以 "Python" 开头
import re

text1 = "Python is fun"
text2 = "I like Python"
pattern = r"Python"

# text1开头匹配
print(re.match(pattern, text1).group())  # 输出：Python
# text2开头不匹配
print(re.match(pattern, text2))  # 输出：None

'''
re.sub ()
'''

# 用指定内容替换匹配到的字符串，支持正则规则替换。示例：将手机号中间 4 位替换为星号
import re

phone = "13812345678"
pattern = r"(1[3-9]\d{2})(\d{4})(\d{4})"  # 分组：前3位、中间4位、后4位

# 用\1和\3引用前后分组，中间替换为****
result = re.sub(pattern, r"\1****\3", phone)
print(result)  # 输出：138****5678

'''
re.split ()
'''

# 根据正则匹配的内容分割字符串。示例：用逗号、分号或空格分割文本
import re

text = "apple, banana; orange grape"
pattern = r"[,; ]+"  # 匹配1个或多个逗号、分号、空格

result = re.split(pattern, text)
print(result)  # 输出：['apple', 'banana', 'orange', 'grape']
5. 正则预编译（re.compile ()）
多次使用同一正则时，预编译可提高效率。示例：重复验证多个邮箱格式
python
运行
import re

# 预编译邮箱正则
email_pattern = re.compile(r"^\w+@[a-zA-Z0-9]+\.[a-zA-Z]{2,}$")

emails = ["test@example.com", "invalid-email", "user123@domain.cn"]
for email in emails:
    if email_pattern.match(email):  # 直接调用编译后的对象方法
        print(f"{email} 是有效邮箱")
    else:
        print(f"{email} 无效")

# 贪婪模式（默认）
尽可能匹配最长的符合规则的字符串。示例：匹配 HTML 标签中的内容（贪婪模式会过度匹配）

import re

html = "<div>内容1</div><div>内容2</div>"
pattern = r"<div>(.*)</div>"  # .* 贪婪匹配任意字符

result = re.search(pattern, html)
print(result.group(1))  # 输出：内容1</div><div>内容2 （过度匹配）

# 非贪婪模式（加？）
尽可能匹配最短的符合规则的字符串（在量词后加?）。示例：修正上述 HTML 标签匹配
import re

html = "<div>内容1</div><div>内容2</div>"
pattern = r"<div>(.*?)</div>"  # .*? 非贪婪匹配

# 用findall获取所有匹配
results = re.findall(pattern, html)
print(results)  # 输出：['内容1', '内容2'] （正确匹配）

# 练习 1：验证日期格式（YYYY-MM-DD）
import re

def is_valid_date(date):
    pattern = r"^\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01])$"
    return bool(re.match(pattern, date))

print(is_valid_date("2023-12-31"))  # True
print(is_valid_date("2023-02-30"))  # False（2月没有30日）

# 练习 2：匹配 URL（如https://www.example.com）
import re

url = "访问 https://www.bilibili.com 或 http://example.org"
pattern = r"https?://www\.\w+\.(com|org|cn)"  # 匹配http/https开头的URL

results = re.findall(pattern, url)
print(results)  # 输出：['com', 'org']（提取匹配的域名后缀）

# 练习 3：筛选特定手机号（最后一位不是 4 或 7）
import re

phones = ["13812345674", "13987654321", "13711112227"]
pattern = r"1[3-9]\d{8}[0-35689]$"  # 最后一位排除4和7

for phone in phones:
    if re.match(pattern, phone):
        print(f"有效手机号：{phone}")  # 输出：13987654321
```



#### json

```python
# 处理json数据
import json

# 字典转JSON字符串
data = {"name": "Alice", "age": 30}
json_str = json.dumps(data, indent=2)
print(json_str)

# JSON字符串转字典
new_data = json.loads(json_str)
print(new_data["name"])  # 输出: Alice
```



#### sys

```python
import sys

# 命令行参数
print(sys.argv)  # 输出传入的命令行参数列表

# Python 版本信息
print(sys.version)

# 退出程序
# sys.exit(0)  # 0表示正常退出
```



### 第三方模块

```python
#由他人编写，需安装使用
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



### 自定义模块

```python
# 创建my_calculator.py
# my_calculator.py（自定义模块文件）

def add(a, b):
    """计算两个数的和"""
    return a + b

def multiply(a, b):
    """计算两个数的积"""
    return a * b

def square(x):
    """计算一个数的平方"""
    return x ** 2

# 模块内测试代码（仅在直接运行模块时执行，导入时不执行）
if __name__ == "__main__":
    print("模块内测试：3+5 =", add(3, 5))
    print("模块内测试：4×6 =", multiply(4, 6))
    print("模块内测试：7的平方 =", square(7))

# 创建main.py,导入my_calculator模块并调用其函数
# main.py（主程序文件）

# 方法1：导入整个模块，通过"模块名.函数名"调用
import my_calculator

print("3+5 =", my_calculator.add(3, 5))  # 输出：8
print("4×6 =", my_calculator.multiply(4, 6))  # 输出：24

# 方法2：导入模块并设置别名（简化调用）
import my_calculator as calc
print("7的平方 =", calc.square(7))  # 输出：49

# 方法3：只导入需要的函数，直接调用函数名
from my_calculator import add
print("10+20 =", add(10, 20))  # 输出：30
```



## 包

```python
# 包是模块的集合（一个包可包含多个模块）
# 包是一个目录,包含了多个.py文件

# 导入原理示例
# __init__.py的作用
一是在导入包时会自动执行文件内容，可利用此特性进行初始化操作，如加载驱动、配置资源等；二是可通过设置

# 定义包的公开接口，只有在这个列表中的模块可以被 from game import * 导入
__all__ = ['characters', 'items']

# 包初始化时执行的代码
print("游戏包已加载")

# 可以在这里定义包级别的变量或函数
VERSION = "1.0.0"

def game_info():
    return f"游戏包版本: {VERSION}"


# 多种导入方式
导入整个包：import game
导入特定模块：from game import characters
导入模块中的特定类：from game.items import Weapon
使用别名：import game.items as gi
```



## 技巧

### 元组拆包

```python
'''
元组拆包:是一种将元组中的元素分别赋值给多个变量的便捷操作。它允许你一次性将元组的各个元素提取出来，赋值给对应的变量，而不需要通过索引逐个访问。
'''
a = 10
b = 90
a,b=b,a

# 嵌套元组拆包
data = ("Alice", (1993, 5, 15), "Engineer")
name, (year, month, day), profession = data
print(year)  # 1993
print(month) # 5

# 其他可迭代对象
# 列表拆包
fruits = ["apple", "banana", "cherry"]
a, b, c = fruits

# 字符串拆包
s = "abc"
x, y, z = s  # x='a', y='b', z='c'

'''
*解决数量不匹配
'''
# 定义一个元组
person = ("Alice", 30, "Engineer")

# 提取第一个元素，剩下的元素打包成列表
name, *details = person
print(name)      # Alice
print(details)   # [30, "Engineer"]

# 提取中间元素，前后元素打包
*info, profession = person
print(info)      # ["Alice", 30]
print(profession)# Engineer
```



