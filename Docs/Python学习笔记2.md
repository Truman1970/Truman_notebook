<!-- TOC -->

- [Python 基础入门](#python-基础入门)
- [字符串](#字符串)
- [列表](#列表)
- [元组](#元组)
- [条件语句](#条件语句)
- [字典](#字典)
- [集合](#集合)
- [for循环](#for循环)
- [while循环](#while循环)
- [函数](#函数)
- [局部变量](#局部变量)
- [全局变量](#全局变量)
- [返回值 return](#返回值-return)
- [文件](#文件)
- [OS](#os)
- [异常处理](#异常处理)
- [Python 路径](#python-路径)
- [pandas与excel](#pandas与excel)

<!-- /TOC -->

<https://www.bilibili.com/video/BV1gt4y1D7W8>  

### Python 基础入门
> print函数自带回车？  

**print的两个参数和转义字符**
- end = '\n'，结束符
- sep = '空格'，多对象分隔符
- `+` ，连接
- `*` ，复制

**注释**
- 单行注释，#
- 多行注释，"""
- 快捷键，`Ctrl` + `/`

**输出**
- 想输出单引号，最外面用双引号
- 想输出双引号，最外面用单引号
- print(r"C:\Android\.android\a.txt")，原样输出

**变量及赋值**
- 变量名支持汉字，由字母、数字和下划线构成，但不能以数字开头，大小写敏感。
- a = 5, b = 1
- a = b = 5
- a,b = 5,1
- 交换赋值：a,b = b,a
- 格式化输出：f'{表达式}'

**input函数**
- input("提示信息")，返回字符型，赋值给一个变量
- 数据类型转换：int(), float(), str()
- 检测数据类型：type()

**算术运算**
- `+`
- `-`
- `*`
- `/`，除，除法返回的都是浮点型（10/2=5.0），type(10/2)
- `//`，整除，不四舍五入
- `%`，取余
- `**`，指数
- `()`，优先级最高

> 比较远算符：`==`,`!=`,`>`,`<`,`>=`,`<=`，返回值是布尔型，只有True和False。   
> and，只要有一个为零，值为0，否则结果为最后一个非零数字。    
> or，所有值都为0，值为0，否则结果为第一个非零数字。  
> not，非0为1，非1为0。  

**优先级排序**
- 1.小括号
- 2.幂运算（指数）
- 3.正负号
- 4.算术运算，先乘除后加减
- 5.比较运算
- 6.逻辑运算，先not后and最后or


### 字符串
> 字符串可以使用单引号、双引号、三引号，三引号支持换行。   
> 输出 I'm a bigtom，可以使用转义字符`\`或者f'{表达式}'。
> input() 需要接收，返回字符型。  

**下标**
- 从0开始
- 标点算一位
- 英文字母算一位
- 一个汉字也算一位

**切片**
- 语法：序列[开始位置下标:结束位置下标:步长]。注：结束位置不包含，步长默认为1。
- 举例：变量[3:5]，变量[3:5:1]，变量[3:5:2]，变量[:]，变量[:25]，变量[0:]，变量[3:5:-1]，变量[3:5:-2]。

**字符串常用方法-find()**
- 查询某个子串是否包含在这个字符串中，如果存在返回这个子串的位置下标，否则返回-1。
- 语法：字符串序列.find(子串,开始位置下标,结束位置下标)。注意：开始下标和结束下标可以省略，表示在整个字符串查找。

**字符串常用方法-index()**
- find()和index()区别：没有匹配到对应字符串，find()返回`-1`，index()报错。

**字符串常用方法-count()**
- 返回某个子串在字符串中出现的次数。
- 语法：字符串序列.count(子串,开始位置下标,结束位置下标)，没有返回0。

**字符串常用方法-replace()**
- 语法：字符串序列.replace(旧子串，新子串，替换次数)。注意：默认是全部替换，如果替换次数超过了子串出现的次数，就替换所有子串。

**字符串常用方法-split()**
- 根据分割字符，将字符串分割成几部分。
- 语法：字符串序列.solit(分割字符,分割次数)。注意：结果中没有分割字符。

**字符串常用方法-join()**
- 字符串连接。
- 语法：连接字符.join(字符串1,字符串2,...,字符串n)

**字符串常用方法-startwith()和endswith()**
- 检查字符串是否以子串开头或者结尾。
- 语法：变量名.startwith(子串,开始位置下标,结束位置下标)。返回True或者False。

**可变类型和不可变类型**
- 数据可以直接修改就是可变，否则就是不可变
  - 可变类型：当变量值改变，id内存地址不变
  - 不可变类型：当变量值改变，id内存地址就改变了
  - 使用id(变量名)可以查询id内存地址
- 可变类型：列表、字典、集合
- 不可变类型：整型、浮点型、字符串、元组



### 列表
定义：变量名 = [数据1,数据2,数据3,数据4]

**查**
- 切片：序列[开始下标位置:结束下标位置:步长]，不包含结束位置。
- index：变量名.index(数据,开始下标位置,结束位置下标)，如果找不到报错。
- count：变量名.count(数据)
- len：返回列表长度，len(变量名)

**增**
- 变量名.append(数据)，列表结尾追加单个数据。
- 变量名.extend(['','',''])，列表结尾追加多个数据。
- 变量名.insert(位置下标，数据)

**删**
- del 变量名，删除整个列表。
- del 变量名[下标]，删除指定数据。
- 变量名.pop(下标)，删除指定下标数据（默认是最后一个），并返回该数据。
- 变量名.remove(数据)，删除列表中某个数据的第一个匹配项。
- 变量名.clear()，清空列表，返回结果是[]。

**改**
- 变量名[1] = '孙悟空'
- 变量名.reverse()，整个列表倒序排列。
- 变量名.sort(reverse=False)，默认升序，降序改成True，首字母大写。

**列表复制**
- 变量名.copy()

**遍历列表**
```python
for i in 变量名:
  print(i)
```


### 元组
特点：元组不能修改，使用小括号。  
定义单个元组：a = (1,)，必须要有逗号。  


**字符串、列表、元组总结**
- 都可以通过下标查询数据，下标从0开始，下标支持负数。
- 都可以通过切片的方式得到一个范围内的数据。
- 数据类型转换：int() float() str() 
- 数据类型转换：list(序列名)，将序列转换为列表。
- 数据类型转换：tuple(序列名)，将序列转换为元组。
  
> 我们将字符串、列表、元组统称为序列。  


### 条件语句
```python
s = input("请输入身高：")
s = int(s)
if s > 10:
    print(f'你的身高大于10')
elif s < 1:
    print(f'你的身高小于1')
else:
    print(f'你的身高是{s}')
```

### 字典
d = {'一加':25,'华为':26,'小米':11,'诺基亚':2}
- 空字典：a = {}，或者 a = dict()
- 字典中元素不重复
- 字典是可变型

**增删改查**
- d[key] = value，如果key存在，则修改对应的值，如果key不存在，新增一个键值对。  
- 删除
  - 删除某一个，del['一加']
  - 删除整个字典 del a 
  - 清空字典，d.clear()
- 查，只能用key查value
  - get()，语法：d.get(key,返回值)，如果key存在，返回value，如果key不存在，如果没有设置返回值，返回None，否者返回设置的返回值。
  - values()，语法：d.values()，返回字典中的所有值。
  - items()，键值对以元组的形式展示。

```python
# 遍历字典中的键
for i in d.key():
  print(i)

# 遍历字典中的值
for i in d.values():
  print(i)

# 遍历字典中的元素，返回：每行是一个元组
for i in d.items():
  print(i)

# 遍历字典中的键和值
for i,j in d.values():
  print(f'{i}={j}')
```

### 集合
- 创建集合可以使用 {} 和 set()，但是创建空集合必须使用set()，因为 {} 创建的是空字典。
- 集合的特点
  - 自动去除重复数据
  - 顺序是随机的，所以不支持下标

**增删改查**
- 增加
  - s.add(数据)，集合自动去重，所以增加内容重复时不进行操作。
  - s.update(数据序列)，数据序列：列表、字符串、元组。
- 删除
  - s.remove(数据)，如果数据不存在，报错
  - s.discard(数据)，如果数据不存在，不报错
  - s.pop()，随机删除集合中某个数据，并返回该数据
- 查
  - 判断数据是否在集合中，print(数据 in 集合名)，返回True或False
  - 判断数据是否在集合中，print(数据 not in 集合名)，返回True或False

**数据类型转换总结**
- int()
- float()
- str()
- list(序列名)，将序列转为列表
- tuple(序列名)，将序列转为元组
- set(序列名)，将序列转为集合

> 集合自动去重，但不支持下标，没有顺序。  


### for循环

```python
a = [1,2,3,4]
for i in a:
  print(i)
```

**break终止循环**
```python
a = [1,2,3,4]
for i in a:
  if i == 2:
    break
  print(i)
# 输出：1
```
> 没有完成循环，条件成立直接推出循环，循环强制结束。  

**Continue退出本次循环，继续执行下次循环**
```python
a = [1,2,3,4]
for i in a:
  if i == 2:
    continue
  print(i)
# 输出：1 3 4
```
> Continue退出本次循环，继续执行下次循环，最终走完整个循环，循环正常结束。  

**for ... else**
```python
a = [1,2,3,4]
for i in a:
  print(i)
else:
  print("循环正常结束才会执行此代码")
```
> 循环正常结束后，才会执行else的语句。continue支持else，但break不支持else。  

**公共操作-enumerate()**
- enumerate()一般用在for循环中，可以将一个能遍历的数据对象（如列表、元组或者字符串）组合成一个索引序列，同时列出数据和数据下标。
- 语法：enumerate(可遍历对象，start=0)，默认下标是0。

```python
a = ['我','是','你','爸爸']
for i in enumerate(a):
  print(i)
# 输出
# (0, '我')
# (1, '是')
# (2, '你')
# (3, '爸爸')
```

```python
a = ['我','是','你','爸爸']
for i,j in enumerate(a,1):
  print(f'下标是：{i}，数据是：{j}')
# 输出
# 下标是：1，数据是：我
# 下标是：2，数据是：是
# 下标是：3，数据是：你
# 下标是：4，数据是：爸爸
```

**列表推导式**
- range(0,11,1)，开始下标默认是0（可以省略），结束下标是11，默认步长为1（可以省略），不包括结束下标。
- 什么是推导式：简化代码代码。

```python
a = []
for i in range(0,11):
  a.append(i)
print(a)

# 等同于

a = [i for i in range(0,11)]
print(a)

# 遍历0-10之间的偶数
a = [i for i in range(0,11) if i%2==0]
print(a)
```

**字典推导式**
```python
# 两个列表合成一个字典
a = ['苹果','橘子','香蕉']
b = [12,23,34]
c = {a[i]:b[i] for i in range(len(a))}
print(c)
```

```python
# 挑出大于30个水果集合
c = {'苹果':12, '橘子':23, '香蕉':34}
d = {i:j for i,j in c.items() if j>30}
print(d)
```

### while循环

```python
i = 1
while i <= 5:
  print(i)
  i = i + 1
```

```python
# break终止循环，直接退出循环。
i = 1
while i <= 5:
  if i == 3:
    break
  print(i)
  i = i + 1
# 输出：1 2
```

```python
# continue
i = 1
while i <= 5:
  if i == 3:
    continue
  print(i)
  i = i + 1
# 死循环
```

### 函数
> 先定义，再调用。  

```python
# 定义函数
def add(a,b):
  # 说明文档内容
  """加法函数"""
  c = a + b
  print(c)
# 调用函数
add(1,2)
# 说明文档调用
help(add)
```

> 位置参数：在定义函数时，参数的名字和位置已经被确定。   

**关键字参数**
```python
def function(姓名,年龄,性别):
  print(f'姓名是{姓名}，年龄是{年龄}，性别是{性别}')

# 传入实参时，明确形参的变量名，参数之间不存在先后顺序。  
function(姓名='张飞',性别='男',年龄=12)
# 调用函数时，如果有位置参数，位置参数必须在关键字参数的前面。  
function('张飞',年龄=12,性别='男')
```

**默认参数**
```python
def function(姓名,年龄,性别='男'):
  print(f'姓名是{姓名}，年龄是{年龄}，性别是{性别}')

# 默认是男，重新赋值才能改变初始值
function('张飞',12)
function('黛玉',16,'女')
```

**可变参数（收集参数）**
```python
def fun(*args):
  print(args)
fun('张飞')   # ('张飞',)
fun('张飞',12)    # ('张飞', 12)
```
> 位置可变参数，接收所有的位置参数，返回一个元组。  

### 局部变量
```python
def fun():
  a = 520
  print(a)
print(a)
# 函数外调用报错
```

### 全局变量
```python
a = 520
def fun():
  print(a)
print(a)
# 函数内外调用都正常。
```

```python
# 修改全局变量，一般不改。
a = 520
def fun():
  # 声明a是一个全局变量
  global a 
  a = 1
  print(a)
fun() # 输出 1
```

### 返回值 return
```python
def add(a,b):
  return a+b
add(1,2)
```
> 遇到return退出当前函数。    

### 文件
<https://www.bilibili.com/video/BV1gt4y1D7W8?p=12>   
```python
文件对象 = open('文件名','访问模式')  
文件对象 = close()  
文件对象.write('内容')  
文件对象.read('num')  
文件对象.readlines()  
文件对象.seek(偏移量，起始位置)  
```

### OS
```python
import os
# 重命名
os.rename('旧文件名','新文件名')
os.rename('旧文件夹名','新文件夹名')
# 删除文件
os.remove('目标文件')
# 创建、删除文件夹
os.mkdir('文件夹名')
os.rmdir('文件夹名')
# 获取当前.py文件所在路径
os.getcwd()
# 改变工作目录到指定目录
os.chdir('aa')
# 获取某个文件夹下所有文件和文件名
os.listdir(目录)
```

### 异常处理
<https://www.bilibili.com/video/BV1gt4y1D7W8?p=13>  


### Python 路径
```python
import os
# 指定工作路径-绝对路径后，可以直接调用文件。
os.chdir('路径')
# 获取当前.py文件路径
os.getcwd()
```
> 路径的字符`\`、`/`、`r`  

**自动路径连接**
```python
# D:\_hiccup\_todo\test.py
import os
P1 = 'D:'
P2 = '\_hiccup'
P3 = '_todo'
路径 = os.path.join(P1,P2,P3)
print(路径)
```

**显示文件夹中所有元素**
```python
import os
# os.chdir('路径')
print(os.listdir())
```
> 另一个遍历函数：os.scandir()  

**判断文件和文件夹**
```python
import os
# os.chdir('路径')
列表 = os.listdir()
for i in 列表:
  print(i,os.path.isdir(i))
  # print(i,os.path.isfile(i))
```

**文件夹和文件筛选**
```python
import os
# os.chdir('路径')
列表 = os.listdir()
文件 = []
文件夹 = []
for i in 列表:
  if os.path.isdir(i) == True:
    文件夹.append(i)
  else:
    文件.append(i)
print(文件)
print(文件夹)
```

**时间戳转换**
```python
import datetime as dt
日期时间 = dt.datetime.fromtimestamp(1592442400)
print(日期时间)
# 当前日期
当前日期 = datetime.now().date().strftime('%Y-%m-%d')
print(当前日期)
# 当前时间
当前时间 = datetime.now().time().strftime('%H:%M:%S')
print(当前时间)
```

**文件属性**
```python
import os
a = os.stat('./README.md')
print(a)
```

### pandas与excel

**DataFrame**

```python
import pandas as pd
r = r'D:\_hiccup\_todo\test.csv'
s = pd.DataFrame({'姓名':[1,2,3],'年龄':[4,5,6],'性别':[7,8,9]})
s = s.set_index('姓名')
s.to_csv(r)
print(s)
```

**read_csv**
```python
import pandas as pd
r = r'D:\_hiccup\_todo\test.csv'
s = pd.read_csv(r)
# 几行几列，不包括表头
print(s.shape)
# 打印列名
print(s.columns)
# 打印索引
print(s.index)
# 打印每列的数据类型
print(s.dtypes)
# 打印内容
print(s)
```
read_csv 参数
- sep = ''，分隔符或者正则表达式 sep = '\s+'
- header = None，没有表头。
- names = []，设置表头，一般和header一起使用
- index_col = ''，设置多个索引用列表
- skiprows，从文件某处开始，需要跳过的行数或行号列表
- encoding，文本编码
- nrows，从文件开头处读入的行数

```python
# txt转换为csv
import pandas as pd
r = r'D:\_hiccup\_todo\test.csv'
r2 = r'D:\_hiccup\_todo\test.txt'
s = pd.read_csv(r)
s.to_csv(r2)
print(s)
```

**read_table**
```python
import pandas as pd
r = r'D:\_hiccup\_todo\test.csv'
s = pd.read_table(r,sep='\s+')
print(s)
```
