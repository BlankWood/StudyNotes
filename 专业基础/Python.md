# Python

## 介绍

python 是一门跨平台, 开源, 免费的解释性高级动态编程语言.  

跨平台: python 编写的码源是跨平台的, 但是部分依赖包或类库不是跨平台的(依赖于特定的系统调用).  

编译与解释: 高级语言按照计算机执行方式的不同分为**静态语言**和**脚本语言**. 执行方式即**编译**和**解释**. 
编译: 将源代码转换成机器语言(一次性).  
解释: 将源代码逐条转换成目标代码(机器语言)同时逐条执行.  


Python 在2008年12月正式发布 Python 3.0 . 其并不兼容之前的版本.  
现在一般使用 3.x 版本.  

## 注释

注释是对程序的解释, 方便自己以及其他人知道这段程序或变量是干什么的, 减少阅读代码的压力.  

- 单行注释: # 加空格后跟注释内容  
`# 注释内容`

-  多行注释: 用上下各三个 " 包围注释内容  
```
"""
注释内容
注释内容
"""
```

## 基础

### 数据类型

| 类型 | 描述 |
| --- | --- |
|数字(Number)|支持int(整数),float(浮点数/小数),complex(复数),bool(布尔)|
| 字符串(String) | 字符序列,一般用""包围的内容为字符串 |
| 列表(List) | 有序的可变序列 |
| 元组(Tuple) | 有序的不可变序列 |
| 集合(Set) | 无序不重复集合 |
| 字典(Dictionary) | 无序的键值对集合 |

### 字面量与变量

- 字面量: 一个固定的值, 如: 2, 2.5, "abc".
- 变量的定义以及赋值:  
`<变量名> = <变量值>`
- 查看变量或字面量的数据类型:  
`type(变量名或字面量)`

### 数据类型转换

```python
int(x)    # 将x转换为一个整数
float(X)  # 将X转换为一个浮点数
str(x)    # 将X转换为一个字符串
# 并不是所有的字符串都可以转换为数字,如:
int("abc")  # 程序将报错
# 浮点数转小数时,会舍弃小数部分
float(1.86) #并不是四舍五入
```

### 标识符

标识符指程序中**变量, 方法, 类**的名字等, 这些统称为标识符.  

规则:  
- 内容限定:  
只允许出现 **英文, 中文(不推荐使用), 数字(不可以在开头), 下划线(_)** 这四类元素.
- 大小写敏感(区分大小写)
- 不可使用关键字: 在程序中一些有特定作用的单词, 称为关键字, 不能用为标识符.

规范:  
命名时需要遵守一点规范,使名字简洁,见名知意

### 运算符

| 加 | 减 | 乘 | 除 | 取整除 | 取余 | 指数 |
| - | - | - | - | - | - | - |
| + | - | * | / | // | % | \*\* |
<br>  

| 运算符 | 描述 |
| --- | --- |
| += | 加法赋值运算符 |
| -= | 减法赋值运算符 |
| \*= | 乘法赋值运算符 |
| /= | 除法赋值运算符 |
| %= | 取模赋值运算符 |
| \*\*= | 幂赋值运算符 |
| //= | 取整除赋值运算符 |

a += b 等效于 a = a + b, 其余同理.  

### 字符串拼接

- 可以通过加号"+"拼接两个字符串(变量).  
- 可以通过将其他数据类型转换成字符串并拼接.  

### 字符串格式化

```python
name = "cba"
message = "my name is %s" % name
# % 为占位符, s 表示将变量变成字符串放入占位的地方

print("my mane is %s, I'm %s years old" % (name, age))
# 多个变量用(),并按顺序放置
```

| 格式符号 | 转化 |
| --- | --- |
| %s | 将内容转换成字符串,放入占位位置 |
| %d | 将内容转换成整数,放入占位位置 | 
| %f | 将内容转换成浮点型,放入占位位置 | 

格式化的精度控制: `%m.nf`(浮点数), `%md`(整数)  
- m,n 为整数.  
- m表示数字的宽度, 不足则在前面补充空格, 宽度超出m则按实践宽度输出.
- n表示小数数位限制, 超出部分四舍五入, 浮点数默认六位小数位.  

`示例: %3.2f, %.1f, %5d`

### 字符串格式化-快速写法

在字符串前加"f"来标识, 然后以{变量}的形式来快速格式化.  
示例:  
```python
name = "abc"
age = 18
print(f"My name is {name}, I'm {age} years old")
```

- 以上两种格式化同样支持表达式.  

### 输入与输出

#### 输入
`<变量> = input()`  
输入的数据为字符串, 如果想要其他类型请使用数据类型转换:  
`a = int(input())`  

input(), 括号内可以添加字符串, 它会在你输入前先输出里面的内容.  
`name = input("请输入你的名字：")`

#### 输出  

`print(内容)`  
输出完后自动换行, 如果不想换行则替换换行符 end=' '.  
`print(内容, end=' ')`  

### 判断语句

#### 布尔(bool)类型数据

表达 真(True) 与 假(False) 的逻辑判断, bool也只有这两种取值, True可以记为 1, False 可以记为 0.  

#### 比较运算符

| 运算符 | 描述 |
| --- | --- |
| == | 判断内容是否相等 |
| != | 判断内容是否不相等 |
| > | 大于判断 |
| < | 小于判断 |
| >= | 大于等于判断 |
| <= | 小于等于判断 |

```python
bool_1 = True
bool_2 = False
print(f"bool_1: {bool_1}, 数据类型为 {type(bool_1)}")
print(f"bool_2: {bool_2}, 数据类型为 {type(bool_2)}")

print(f"1 == 2 的结果是: {1 == 2}")
print(f"1 != 2 的结果是: {1 != 2}")
```

#### 判断语句基本格式

```python
# if <判断条件>:  
#     <条件成立时执行的语句>  
# else:  
#     <不成立执行的语句>  

# ---------------示例-----------------

age = int(input("请输入你的年龄:\n"))

# 注意语句缩进, python以此来判断代码块的归属关系.
if age >= 18:
    print("你已经成年了")
    print("该学会自己敲代码了")
else:
    print("你还未成年")
    print("需要进行未成年游戏时长限制")
```

elif(else if):

```python
age = int(input())

if age > 10:
    print("10岁以下")
elif age > 20:
    print("10~20岁")
elif age > 30:
    print("20~30岁")
else:
    print("30岁及以上")
```

- 判断语句可嵌套, 即执行的语句内也可以在加入判断语句.

### 循环
#### while循环

- 基础语法
```python
# while 循环条件 :
#     循环体,一条或多条语句

# ---------示例---------

i = 1
while i < 10 :
    print(f"第{i}次输出")
    i += 1
print("输出完毕")
```
- 注意别设置成死循环
- while循环可嵌套

#### for循环

python中的for循环相当于是Java, c++中的 for each, 对一个集合(序列)中的元素逐个遍历.  

- 语法:
```python
# for 临时变量 in 待处理数据集 :
#     循环体

# ---------------示例----------------

str1 = "collection"
for c in str1 :
    print(c + ' ', end = ' ')
```

- range
```python
range(num) #获取0到num的数字序列, 不包含num
range(num1, num2)  #获取num1到num2的数字序列, 不包含num2
range(num1, num2, step)  #获取num1到num2, 步长为step的数字序列, 不包含num2

# ----------示例----------

for i in range(0, 20, 3):
    print(i)
```

- for循环可嵌套
- for与while可相互嵌套

#### continue与break

- continue : 执行时结束本次循环, 直接进入下一次循环.
- break : 执行后跳出循环,剩下的循环也不再执行.

```python
for i in range(10):
    if i%2 == 0 :
        continue
    for j in range(10):
        if i == j :
            break
        print(str(j) + " ", end=' ')
    print()
```

### 函数

函数: 可重复调用, 用以实现某种特定功能的代码块。

- 函数的定义：  
```
def 函数名([传入参数]):
    函数体
    [return 返回值]
```
- 调用：`函数名([传入参数])`

```python
# 参数与c++和Java语法不同，不需要声明参数类型
def add(x, y)
    """
    有两个参数，计算两数之和，进行输出，并返回和。
    在写函数时记得写说明文档
    """
    res = x + y
    print(f"{x} + {y} = {res}")
    return res

# 调用
result = add(1, 1)
print(result)

# 当函数无返回值时会返回 None，类似于Null，表示空或返回值无意义。 
```

- 函数可嵌套调用。
- 在函数内定义的变量为局部变量，作用域只有其函数内部。加上关键字 global 可使局部变量声明为全局变量。


#### 多返回值

在return时将多个返回值用 "," 隔开, 即可返回多个返回值. 在接收时也需要多个变量接收, 也用 "," 隔开.

#### 多种参数

1. 位置参数: 调用函数时根据函数定义的参数位置来传递参数.
2. 关键字参数: 函数调用时通过 "键=值" 的形式传递参数, 这样可以不用按写定的顺序传参.  
`user_info(name='甲', age=19, gender='男')`
- 位置参数与关键字参数可混用, 传入时位置参数需要在关键字之前.
3. 缺省参数(默认参数): 在定义函数时设置默认值, 不传入此参数即用默认值, 定义时有默认值的参数需要写在没有默认值参数的后面.
4. 不定长参数: 在定义函数时在参数前加上 "*" ,表示可接收任意数量的参数, 函数接收后形成元组, 如果加上 "**" ,传入参数应为"key=value"的形式, 函数接收后形成字典.

#### 函数作为参数

函数作参数一般用作对复杂数据类型(类与结构体)的比较规则的定义等, 使调用时自定义比较规则.(个人经验)

- lambda匿名函数  

作为参数的函数一般不会过于复杂,也不会多次调用, 为了简化书写使用匿名函数, 而不用def定义.

- 定义:  
	lambda 传入参数: 函数体  
	> lambda函数一般比较简短, 不超过一行.  
	> 默认返回函数体的计算结果.

[常用内置函数](#常用内置函数)  

### 数据容器

可以容纳多份数据的容器。

| 容器 | 有序存储(下标) | 元素可以重复 | 元素可以修改 |
| --- | --- | --- | --- |
| 列表(list) | o | o | o |
| 元组(tuple) | o | o | x |
| 字符串(str) | o | o | x |
| 集合(set) | x | x | o |
| 字典(dict) | x | x | o |

- max(容器), 获取容器中最大元素.
- min(容器), 获取容器中最小元素.
- list(容器), str(容器), tuple(容器), set(容器) 转换成对应容器,字典只保留Key(除了转为字符串).
- sorted(容器, [reverse=Ture]), 对容器进行排序返回列表, 后一个参数表示降序.

#### 列表(list)

##### 定义  

1. 变量(列表)名称 = [元素1, 元素2, 元素3, 元素4, ...]
2. 空列表：变量名 = [] 或 变量名 = list()
- 列表的元素的数据类型可以不同。
- 支持嵌套。

##### 下标索引
- 列表可以通过下标访问数据，每个元素的下标按顺序从0开始依次递加。
- 负数下标(反向索引)：指从后往前，最后的元素索引为 -1，向前递减。

```python
Mylist = [[1,2,3,4,5],[6,7,8,9,10],[11,12,13,14,15]]
print(Mylist[0][3])     # 4
print(Mylist[-1][0])    # 11
# 访问"不存在的数据"时会报错。
```

##### 常用方法

| 方法 | 作用 |
| --- | --- |
| index(元素) | 获取第一个对应元素的下标，如果不存在则会报错 |
| *列表名[下标] = 值 | 对指定下标位置的元素进行重新赋值 |
| insert(下标, 元素) | 在指定下标位置插入元素 |
| extend(容器) | 将其他容器中的元素添加至列表尾部 |
| *del 列表名[下标] | 删除指定下标的元素 |
| pop(下标) | 删除指定下标的元素, 返回删除的元素 |
| remove(元素) | 删除第一个对应元素 |
| clear() | 清空列表 |
| count(元素) | 添加指定元素的数量 |
| *len(列表名) | 获取列表的元素数量(长度) |

- 使用: `列表名.方法(参数)`

##### list的遍历

- while循环  
```
index = 0
while index < len(列表):
    ...
    index += 1
```

- for循环  
```
for element in 列表:
    ...
```

#### 元组

元组定义之后, 不允许修改.  

##### 定义

1. 变量名 = (元素1, 元素2, 元素3, ...)  
2. 空元组: 变量名 = () 或 变量名 = tuple()
- 如果只有单个元素则也要加",": `t = (23,)`
- 可嵌套, 支持索引

##### 方法

1. index(元素)
2. count(元素)
3. len(元组)

##### 遍历

1. while
2. for

与list基本一致

#### 字符串

字符串是存放字符的容器, 可存放任意长度的任意字符.  

- 支持索引, 无法修改.  

##### 方法

| 方法 | 说明 |
| --- | --- |
| index(字符串) | 查找指定字符串的下标 | 
| replace(字符串1, 字符串2) | 将字符串中所有的字符串1替换成字符串2,得到新字符串 |
| split(分隔符字符串) | 按指定的分隔符字符串将其分割, 返回一个列表 |
| strip([字符串]) | 去除字符串前后的指定字符串, 不填参数即去除空格 |
| count(字符串) | 统计指定字符串的数量 |
| len() | ... |

#### 有序容器的切片

`序列[起始下标:结束下标:步长]`  
- 从序列的起始位置按步长取出元素,到结束位置.  
- 三个参数都可以省略, ":"不能省.  
- 步长可为负数, 表示反向取, 此时起始于结束下标也要反向标记.  

#### 集合

##### 定义

1. 变量名 = {...}
2. 空集合: 变量名 = set() ({}的方式被字典占用了)
- 无序(不支持索引), 允许修改元素, 不允许元素重复.

##### 方法

| 方法 | 注释 |
| --- | --- |
| add(elem) | 添加元素 |
| remove(elem) | 删除指定元素 |
| pop() | 随机删除并返回元素 |
| clear() | ... |
| difference(集合2) | set3 = set1 - set2, 原集合不变 |
| difference_update(集合2) | 取差集, 更新原集合 |
| union(set2) | 返回合并的集合,原集合不变 |
| len() | ... |

##### 遍历

只支持 for 遍历.

#### 字典 

字典存储的元素为键值对, 无序.
- 键值对: `key : value`, 键(key)不可重复, key 可以为字典之外的其他数据类型, 值(value)无限制.

##### 定义

1. 变量名 = {key: value, key: value, ...}  
2. 空字典: 变量名 = {} 或 变量名 = dict()

- 取值: `字典名[key]`, 用key代替索引取值.
- `字典名[key] = value`, 如果key已存在则更新value, 否则新增键值对.

##### 方法

| 方法 | 作用 |
| --- | --- |
| pop(key) | 根据key删除元素并返回 |
| clear() | 清空 |
| keys() | 获取key序列 |
| len() | ... |

##### 遍历

1. 通过Keys() 获取key序列, 再通过for循环用key获取value.
2. for循环遍历字典得到key, 取出键值对中的value. 



### 文件读写

#### 打开文件

`open(name, mode, encoding)`  
- name: 为要打开的目标文件的文件名(包含文件路径)
- mode: 设置打开文件的模式(访问模式): 只读, 写入, 追加等
- encoding: 编码格式(推荐UTF-8)  

`f = open("D:/Python.md", "rt", encoding="UTF-8")`
- encoding的顺序并不是第三位(open()的参数非常多), 需要用关键字指定.

| 模式 | 描述 |
|---- | --- |
| r | 只读模式(默认) |
| w | 写入, 原有内容会被删除, 如果不存在, 则先创建文件 |
| a | 追加, 将新的内容写入末尾, 文件不存在则先创建文件 |
| t | 默认, 文本文件, 以文本形式读出, 写入 |
| b | 二进制文件, 以二进制读出, 写入 |

#### 读取文件

- 对同一个文件对象, 多次重复读取时会从上一次结束的位置开始读取, 而不是从头开始.  

| 方法 | 说明 |
| --- | --- |
| read(num) | num表示从文件中读取的数据长度(单位:字节), 没有传入num, 表示读取所有数据. |
| readlines() | 按行的方式读取整个文件的数据, 返回一个列表, 每一行数据为一个元素 |
| readline() | 读取一行数据 |

```
f = open("D:/test.txt", "r", encoding="UTF-8")
t = f.readline()
for s in t:
    print(s)
```

- for循环读取文件
```
for line in file:
    print(line)
```

#### 关闭文件

如果不关闭文件, 文件会一直程序占用.

`f.close()`

- with open: 执行完成后会自动关闭文件
```
with open(...) as f:
    ...
    ...
```

#### 文件写入

`f.write(...)`: 将内容写入文件(缓存区).  
`f.writelines(...)`.  
`f.flush()`: 将缓冲区内容真正写入文件(关闭文件也可以完成此操作), 避免频繁操作硬盘, 提升效率.


### 异常

程序中出现的错误, 会使程序无法继续运行, 会退出运行并给出错误信息.

#### 捕获异常

异常(bug)难以预测, 也不可能完全杜绝. 捕获异常能使程序出现异常时能够继续运行, 并进行一定程度的处理.

```
try:
    可能出现异常的代码
except [异常类别 as 异常的名称]:
    如果出现了异常执行的代码
else:
    未出现异常所执行的代码
finally:
    无论是否出现异常都会执行的代码

---------示例----------

try:
    a = 1/0
except ZeroDivisionError as e:
    print("0不能作除数")
    print(f"异常信息: {e}")
```
- 指定了异常类别后, 只会捕获指定类别的异常, 多个异常类别写在括号内, 用逗号隔开.  
- Exception 异常包含了所有异常类别.

#### 异常的传递

出现异常的函数会把异常抛给调用此函数的函数或程序, 调用此函数的函数或程序可以捕获到异常, 不一定需要在出现异常的位置进行捕获.

### 模块

Python 模块(Module), 是一个 Python文件(.py), 里面有已经写好的类, 函数, 变量等, 可以直接导入后使用, 不需要自己写.

#### 导入模块

所有导入语句一般会全都写在文件开头.

`[from 模块名] import [模块 | 类 | 变量 | 函数 | *] [as 别名]`  
一般用法:
`import 模块名`  
`from 模块名 import [类|函数|变量|*]`

只导入模块时使用函数等需要通过: `模块名.函数名()` 的方式, 如果直接导入函数则可以省略模块名直接调用函数.

#### 自定义模块

每一个自己写的python文件都可以作为模块导入到其他文件

- `__name__`: 这是文件自带的变量, 当右键运行程序时变量值会变成 `__main__`, 一般利用此变量隔离自定义模块中的测试调用, 直接写`main`, 回车即可.

- 不同模块的同名功能, 后导入的会覆盖先导入的

### Python包

一个Python包中包含多个模块文件, 用Python包来管理模块文件

#### 导入

`import 包名[.模块名.功能名]`

- `__init__.py`: 有此文件的包才可以被导入, 可以为空, 但不能没有.
- `__all__`: "\__init__.py"文件中的此变量可以控制 `import *` 时可导入的模块, `__all__ = [模块名]`

#### 安装第三方Python包

需要使用Python内置的pip程序, 使用命令提示符(cmd), 需要先到目录下或添加环境变量, 通过 `pip install 包名` 来下载第三方包.

国外网站下载较慢, 需要指定一个国内网站:  
`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 包名`

永久更换: `pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple`  

编程工具中也有提供下载第三方包的方法(PyCharm):  
"设置 -> Python Interpreter -> + -> 勾选Option -> -i https://pypi.tuna.tsinghua.edu.cn/simple"

### 数据可视化图表

#### json数据格式

json为一种轻量级的数据交互格式, 按特定格式组织和封装数据, 本质为特定格式的字符串.  
json在各种编程语言中流通, 进行不同语言数据传递与交互.
json的格式与Python中的字典一致, 或者是由字典组成的列表.

```
import json

data = [{"name": "张三", "age": 21}, {"name": "李四", "age": 23}]

# 数据转json, 后一个参数阻止转为ASCII码, 避免中文乱码
json_str = json.dumps(data[, ensure_ascii=False])

# json转数据
json_data = json.loads(json_str)
```

#### pyecharts模块

由百度开源的数据可视化, 官网: `pyecharts.org`, 画廊: `gallery.pyecharts.org`

#### pyecharts入门

`line = Line()`: 获取折线对象.

| 方法 | 说明 |
| --- | --- |
| add_xaxis(data) | 添加横坐标, 数据为列表 |
| add_yaxis(name, data) | 添加纵坐标, name为纵坐标所代表的意义 |
| reader() | 生成二维折线图 |
| set_global_opts() | 设置全局配置, 具体使用自行查阅官网 |

`map = Map()`: 获取地图对象.

| 方法 | 说明 |
| --- | --- |
| add(name, data, maptype) | name为地图的名字, data格式..., 地图类型默认为中国地图(china) |
| reader() | 生成地图 |
| set_global_opts() | 设置全局选项, 具体设置参数请移步官网说明文档 |

`bar = Bar()`: 获取柱状图对象.

| 方法 | 说明 |
| --- | --- |
| add_xaxis(data) | 添加x轴数据 |
| add_yaxis(name, data) | 添加y轴名称与数据 |
| reversal_axis() | 反转xy轴 |

`timeline = Timeline()`:    时间线对象.  
`add(Bar, name)`:           将柱状图加入时间线.  
`add_schema()`:             添加各种模式设置参数.  


## 变量作用域

作用域又可以称为命名空间, 指变量起作用的范围.  
Python中有四种变量作用域: 局部作用域(Local), 嵌套作用域(Enclosed), 全局作用域(Global), 内置作用域(Built-in).  
作用域中变量的调用顺序为就近原则: LEGB.  

只有 **模块, 类, 函数** 会在全局作用域中引入新的作用域.  

- 局部作用域:  
    函数内部即局部作用域, 其内部赋值变量会定义成局部变量(即使此变量名称已在全局变量中), 局部变量不可在函数外部调用.  
    在函数内(局部作用域内)可调用全局变量(按调用顺序). 但为其赋值视为定义新的局部变量, 而不是改变全局变量. 此时, 不能在赋值前调用此变量, 否则报错.  
    如果需要在函数内部修改全局变量, 需要先用 global 关键字声明.  

    ```python
    s = "hello world"

    def test():
        # print(s)
        # global s
        s = "HELLO WORLD"
        print(s)        

    test()
    print(s)
    ```


- 嵌套作用域:  
    指在函数内部定义一个函数, 外层函数的作用域称为嵌套作用域.  
    内部函数可调用外部函数的变量(调用顺序).  


- 全局作用域:  
    指一个 py 文件内, 或者说是一个模块内.  


- 内置作用域:  
    python 语言内置的模块, 如 print 等关键字.  



## 常用内置函数

- filter(function, iterable):  
    用于过滤序列, 即筛选元素, 返回符合条件的新列表.  

    - 参数:    
        function: 判断函数.  
        iterable: 可迭代对象.  
        将容器中的元素传入判断函数, 保留结果为 True 的元素.  
    
    - 返回值:  
        一个容器: filter.  

示例:  
```python
num = [1, 2, 3, 4, 5, 6, 7, 8, 9]
odds = filter(lambda x: x%2==0, num)
for i in odds:
    print(i, end=" ")
```

- eval(express):  
    执行字符串表达式, 并返回其结果.  

示例:  
```python
two = eval("1+1")
l = eval("[1, 2, 3, 4, 5]")
def add_ten(x):
    return x + 10

a = 10
a = eval("add_ten(a)")
```


- map(function, iterable, ...):  
    将容器每个元素调用函数, 获取其返回值序列.  
    即批量处理.  

    - 参数:  
        function: 此函数的参数数量应与后面的容器个数相同.  
        iterable: 一个或多个序列, 其大小(size)应一致, 否则按最小size处理.  
    
示例:  
```python
num_list = list(map(int, input().split()))
"""
输入: 1 2 3 4 5 6 7 8 ...
input() 获取输入的字符串后, 用split()分割得到字符串列表.
通过 map 对其中每一个字符串调用 int 函数转为数字.  
用 list() 将返回的 map 对象转为列表.  
"""
```

- reduce(function, iterable):  
    在 functools 模块中.  
    将 iterable 中的元素进行累积: 先将容器中第 1, 2 个元素应用于 func, 再将其结果与第三个元素应用于 func, 以此累积.  

    func 应有两个参数, 一个返回值.  

例:  
`sum = reduce(lambda x, y: x + y, [1, 2, 3, 4, 5])`



## 类与对象

类(class), 对某种事物的属性与行为的抽象与封装, 人类, 学生类, 教师类, 动物类, 猫类等.  
对象: 由类(设计图)创建出来的实体.  

一个类包含:  
1. 属性, 即定义在类中的变量(成员变量)  
2. 行为, 即定义在类中的函数(成员方法)

成员方法的定义:  
`def 方法名(self, 参数...)`  
self表示类对象本身(相当于c/java的this), 定义时必须写, 调用时可忽略.  

```
class Student:
    name = None
    age = None

    def say_hello(self):
        print(f"Hello everyone, I'm {self.name}")
```

创建对象: 变量 = 类名(), `stu = student()`

### 构造方法

在创建对象(构造类)时自动执行的方法, 可以设置参数以便初始化类对象属性.  

构造方法: `def __init__(self, 参数...)`  
```
def __init__(self, name, age)
    self.name = name
    self.age = age
```

self 为 __new__方法返回的实例对象, 代表对象的空间. 可以取其他名字(如cls, this), 但一般用self. 其先于 __init__执行.  
可以通过重写其来实现单例模式.  

对应的有析构方法, 在删除对象(del)时会进行调用.  
`def __del__(self)`


### 类属性与实例属性

类中的属性分为**实例属性**与**类属性**.  
实例属性为实例对象的属性, 同类不同对象的实例属性不同, 一般全在 __init__方法中定义.  
类属性为此类共享的属性, 同一个类属性相同, 定义在类的开头.  



### 魔术方法

内置的类方法被称之为魔术方法.  

1. `__init__`
2. `__str__`: 相当于Java的toString, print()(转换成字符串时)时会执行此方法, 未写则会打印地址.  
3. `__lt__(self, another)`: > 或 < 比较时进行的判定规则.  
4. `__le__(self, another)`: > = 比较时的判断.  
5. `__eq__(self, another)`: = 相等比较的判断, 未写时根据地址判断.

### 封装

- 私有成员变量/方法  
在类中以 "__" 开头的变量/方法即为私有, 私有变量和方法不能在类外部调用, 不可继承, 仅可类内部的各方法自己调用.   

### 继承

继承方式: `class 类名(父类名, 父类2, ...): `, 继承的类被称为子类.  
继承之后子类拥有父类的**非私有**成员变量与方法, 重名的变量与方法只会保留先继承(继承时靠左边)的那个类.  

- Pass: 如果类内容无需其他内容, 则可以写上Pass, 表示无内容, 防止语法错误.  

python中不存在方法的重载, 后者会覆盖前者.  
重名的方法与属性的查找(解析)顺序称为 MRO. 采用 C3 算法来得到 MRO.  
- C3算法:  
    类C 的MRO记为 L[C] = L(C1, C2, C3 ...). C1 为头, 其余为尾.  
    如果类C 继承父类 B1, B2,...,BN. L[C(B1, B2,...,BN)] = C + merge(L[B1], L[B2], ... , L[BN], B1, B2,...,BN).  
    merge: 从前往后, 检查每个元素是否出现在其他元素的尾部. 没有则将其输出, 并在所有元素中删除.  

#### 复写

复写指子类重新定义父类中已有的属性/方法.  

调用继承的父类变量与方法:  
1. 父类名.变量/方法(self)
2. super().变量/方法

#### 变量类型注解

方便第三方工具, 编译器, 程序员等确定参数, 返回值类型. 一般会在不能直接判断出数据类型时进行注解. 注解与实际不符时不会报错.  

- `变量: 数据类型`:  
```
a: int = 4
studentlist: list[Student]
gradedict: dict[str : int]
```

- `变量     # type: 数据类型`:  
```
var_1 = 6           # type: int
var_2 = func()      # type: list[str]
```

#### 函数(方法)类型注解

```python
def add(x: int, y: int) -> int: # 返回值类型
    return x + y

print(add("你好", ", unwelcome"))   # 完全没问题
```

#### Union类型

`Union(int, str)`: 表示可能是int或str, 用于数据类型注解.  

### 多态

不同子类继承同一个父类时, 都对父类的同一方法进行复写, 此时不同子类调用同一个父类方法, 会得到不同结果.  

```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        print("汪汪汪")

class Cat(Animal):
    def speak(self):
        print("喵喵喵")

def animalSpeak(animl: animal)
    animal.speak()

dog = Dog()
cat = Cat()

animalSpeak(dog)
animalSpeak(cat)
```

#### Mixin

通过定义一个共同的基类(父类)来拓展其他类的功能.  
这种类称为 Mixin类, 一般在继承时放在前面, 避免被覆盖.  
类似于接口.  


### 重载构造方法

由于 python 不支持方法的重载, 所以不能直接进行重载.  
虽然也能用不定参数或默认参数, 然后按不同情况进行不同的处理, 但阅读, 维护的难度较大.  
可以使用装饰器间接进行重载.  [装饰器详解](#装饰器).  

- @classmethod:  
    @classmethod 允许在不实例化类的情况下访问该方法(类方法).  
    用于重载时, 此类函数称为工厂方法.  

    在其修饰的方法中加入参数 "cls", cls表示调用该方法的类名, 因此可以通过其调用原本的构造方法, 其名称可更改(不推荐).  
    其他的参数 parameter2 需要符合构造方法的参数.  
    
    ```py
    @classmethod
    def func(cls, parameter1):
        ...
        return cls(paramete2)

    c = ClassName.func(parameter)
    ```


## 装饰器

在给函数进行功能增强时, 可以使用装饰器. 通过在函数前加上 `@<装饰器名>` 的方式使用.  


### 闭包

闭包即在函数内定义函数, 并引用外部函数的变量.  

```python
def outer(x):
    def inner(y):
        return x + y
    return inner


print(outer(3)(4))
# 调用outer时, 得到返回值inner; 再调用inner得到返回值x+y.  
```


### 装饰器

装饰器即闭包的应用.  
将原函数作为参数传入, 在内部定义新函数为其添加功能后, 将新函数返回.  

```python
def outer(func):
    def inner():
        print("Before func()...")
        func()
        print("After func()...")
    return inner


def hello():
    print("hello world!")


hello = outer(hello)
# 调用outer得到返回值inner(一个函数), 将其赋值给hello.
hello()

# 改用装饰器写法
@outer
def world():
    print("hello world!")


world()
```

- 加上参数和返回值:  
```python
def test(Instruction):
    # 接收装饰器参数 Instructions
    def out_wrapper(func):
        # 接收函数
        # @functools.wraps(func)
        def wrapper(*args, **kwargs):
            # 接收函数的参数, 进行功能增强, 并返回函数返回值
            print(Instruction)
            result = func(*args, **kwargs)
            return result
        # 返回后函数的名字(func.__name__)会变成 "wrapper", 可以用另一个装饰器解决(functools.wraps(func)) ...
        return wrapper

    return out_wrapper


@test(Instruction="func call successfully")
def add(x, y):
    return x + y


x = add(3, 4)
print(x)
```

- 装饰器还可以用类实现, 不一定是函数.  
```python

class Prompt:
    def __init__(self, prompt):
        self.prompt = prompt

    def __call__(self, func):
        def wrapper(*args, **kwargs):
            print(self.prompt)
            result = func(*args, **kwargs)
            return result

        return wrapper


    # 在初始化中还可以直接加func, 则装饰器本身没有参数
    # def __init__(self, func):
    #     self.func = func

    # def __call__(*args, **kwargs):
    #     return self.func(*args, **kwargs)


@Prompt(prompt="time:")
def print_time(time):
    print(time)


print_time("now")
```

- 装饰器可以叠加.  
- 装饰器可以修饰类, 只有在实例化的时候生效一次.  


## Mysql

python连接MySQL需要使用第三方库: pymysql.  

```python
from pymysql import Connection

# 获取到Mysql数据库的连接对象
conn = Connection(
    host="localhost",   # 主机名(或IP地址)
    port=3306,          # 端口, 默认3306
    user="root",        # 账户名
    password="....",    # 密码
    [autocommit=Ture]   # 设置自动提交
)

# 获取游标对象
cursor = conn.cursor()

# 选择数据库
conn.select_db("数据库名")

# 执行SQL语句
cursor.execute(SQL语句)

# 获取查询结果
result: tuple = cursor.fetchall()
for roll in result:
    print(roll)

# 手动提交事务
conn.commit() 

# 关闭连接
conn.close()
```


## 重载运算符

python中可以通过重写魔术方法(内置方法)的方式改变运算符的行为.  
以此实现自定义的运算符.  

| 运算符 | 特殊方法 |
| --- | --- |
| +(一元) | `__pos__` |
| -(一元) | `__neg__` |
| not(一元) | `__not__` |
| +(二元) | `__add__` |
| -(二元) | `__sub__` |
| * | `__mul__` |
| / | `__truediv__` |
| % | `__mod__` |
| ** | `__pow__` |
| == | `__eq__` |
| != | `__ne__`  |
| > | `__gt__` |
| < | `__lt__` |
| >= | `__ge__` |
| <= | `__le__` |
| and | `__and__` |
| or | `__or__` |

- 一元运算符与二元运算符:  
    一元即对一个对象进行操作, 如: +5, -9...  
    二元即对两个进行操作: list + list...  

示例:
```py
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        if isinstance(other, Vector):
            new_x = self.x + other.x
            new_y = self.y + other.y
            return Vector(new_x, new_y)
        else:
            raise TypeError("Unsupported operand type.")

# 创建两个 Vector 实例
v1 = Vector(1, 2)
v2 = Vector(3, 4)

# 使用加法运算符相加
result = v1 + v2

# 输出结果
print(result.x, result.y)  # 输出: 4 6
```


# PySpark的简单使用

Spark是Apache基金会旗下的顶级开源项目, 用于对海量数据进行大规模分布式计算.PySpark是Spark提供的python第三方库, 用于Spark开发, 也可以将程序提交的Spark集群环境中, 调度大规模集群进行执行.  
Spark是大数据开发的核心技术.  




# python爬虫


## 简单的爬虫架构

- 三大模块:  
    URL管理器: URL队列管理, 防止重复爬取.  
    网页下载器: 网页内容下载.  
    网页解析器: 提取价值数据, 提取新的待爬URL.  


## requests 库

发送请求:  
requests.get/post(url,params,data,headers,timeout,verify,allow_redirects,cookies)  
    - url: 目标网页的URL.  
    - params: 字典形式, 设置url后面的参数.  
    - data: 字典或字符串, 一般用于post方法时提交数据.  
    - headers: 设置user-agent, refer等的请求头.  
    - timeout: 超时时间, 单位: s.  
    - verify: 是否进行Https证书验证, 默认Ture.  
    - allow_redirects: 是否让resquest做重定向, 默认Ture.  
    - cookies: 附带本地的cookies数据.  

接收响应:  
```python
r = requests.get/post(url)
# 状态码, 200 表示请求成功
r.statues_code
# 当前编码 (requests 会根据Headers推测编码, 推测不到则设置为 ISO-8859-1 可能导致乱码)
r.encoding
# 返回的网页内容
r.text
# 返回的 HTTP 的 headers
r.headers
# 实际访问的URL
r.url
# 以字节的方式返回内容
r.content
# 服务端要写入本地的cookies数据
r.cookies
```

- 测试:  
```python
import requests

url = "https://www.baidu.com"

r = requests.get(url)

print(r.status_code)
print(r.headers)
print(r.encoding)
# 乱码处理: 一般编码方式在 text 中有写, 把 r(respond)的属性 encoding 更改为对应编码, 再次输出即可.  
print(r.text)
r.encoding = "utf-8"
print(r.text)
```

## URL管理器

对外接口: 取出一个待爬取URL, 新增待爬取URL.  
实现逻辑: 取出时状态改成"已爬取", 新增时判断是否已经存在.  
数据存储: python内存, redis, MySQL. 两个集合(已爬取和待爬取).  

实现:  
```python
class UrlManager():
    """
    url管理器类
    """

#   初始化两个 set 集合, 用于存放 待爬取的url 和 已爬取的url
    def __init__(self):
        self.new_urls = set()
        self.old_urls = set()

#   添加 url 至 待爬取 url 集合中
    def add_new_url(self, url):
        if url is None or len(url) == 0:
            return
        if url in self.new_urls or url in self.old_urls:
            return
        self.new_urls.add(url)

#   批量添加 url
    def add_new_urls(self, urls):
        if urls is None or len(urls) == 0:
            return
        for url in urls:
            self.new_urls.add(url)

#   取出 url
    def get_url(self):
        if not self.isEmpty():
            url = self.new_urls.pop()
            self.old_urls.add(url)
            return url
        else:
            return None

    def is_empty(self):
        return len(self.new_urls) == 0

```

## Beautiful Soup 库

得到的响应数据一般为网页, 需要对其进行解析.  
因此可以使用 Beautiful Soup 第三方库(beautifulsoup4), 从HTML中提取数据.  

步骤:  
- 创建 BeautifulSoup 对象  
    soup = BeautifulSoup(html_doc, 'html.parser', from_encoding)
    - html_doc: HTML文档字符串.  
    - features: 解析器, 'html.parser' 为 python 的标准 HTML 解析库.  
    - from_encoding: 编码格式.  

- 以标签名来搜索节点:  
    soup.find/find_all(name, attrs, string)  
    - name: 标签的名称.  
    - attrs: 字典类型, 根据属性值筛选.  
    - text: 根据文本内容进行筛选.  


## 对目标网站分析

访问网站得到的响应信息分为两种: 网页信息(HTML) 和 json数据.  
当一个网页的内容较大时, 数据不会一次性全部传输过来, 只会先传输其网页架构等, 即异步加载.  
其他的, 如视频, 评论等会先贴上存放其的网址, 另传输数据包(json数据).  

对于复杂的网页, 要先对其进行分析, 找到想要的数据的位置.  

进入目标网站, 右键 -> 查看页面源代码/检测.  

在检测中找到 "网络"(network), 刷新页面, 可以看到有大量的数据传送过来.  
在其中找到数据的位置(抓包).  

在数据的请求头中可以看到其 请求方式(post/get) 和 URL.  
并对 HTML 或 json 进行分析找到需要的数据的精确位置, 然后才能在编写代码时能够精确地提取出来.  






