<!-- TOC -->

- [print](#print)
- [数学运算](#数学运算)
- [自变量](#自变量)
- [while](#while)
- [for](#for)
- [if](#if)
- [def 函数](#def-函数)
- [Global 和 Local](#global-和-local)
- [读写文件](#读写文件)
- [参考链接](#参考链接)

<!-- /TOC -->



环境：3.9版本  
### print

```python
print("hello world"),
print('hello world')
print("I'm papa")
print('I\'m papa')
print("hello" + "world")
print("oneplus" + " 9")
print("oneplus" + str(9))
print(1+2), 3
print('1+2'), 1+2
print(int('1')+2), 3
print(float('1.2')+2)
```


### 数学运算
```shell
1+1, 2
1-1, 0
2*2, 4
2**10, 1024
8%2, 0 
9//4, 2(取整)
```

### 自变量
```python
a = 2
print(a)
b = 2**2
print(b)
```
```python
a,b = 2,4
print(a,b)
```

### while
```python
#注意冒号
c = 1
while c < 10:
    print(c)
    c = c + 1
```

### for
```python
#注意冒号
example_list = [1,2,3,4,5,6,7,8,13]
for i in example_list:
    print(i)
```

```python
#注意冒号
#1-9
for i in range(1,10):
    print(i)
#1,4,7
for i in range(1,10,3):
    print(i)
```
> 小技巧：若是语句前有很多空格或者TAB，选中对应语句，windows中用'Crtl' + '['，可恢复默认格式。  


### if
```python
#hello
a,b,c = 1,2,0
if a<b>c:
    print("hello")
#hello
a,b,c = 1,2,0
if a != c:
    print("hello")
```

```python
#world
a,b,c = 1,2,0
if a<c:
    print("hello")
else:
    print('world')
```

```python
#a=1
a = 1
if a>1:
    print("a>1")
elif a<1:
    print("a<1")
else:
    print('a=1')
```

### def 函数
```python
def function():
    print('This is a function')
    a = 1
    print('a')
function()
```
```python
#1024
def function(a,b):
    c = a**b
    print(a,'^',b,'=',c)
function(2,10)
```

### Global 和 Local

```python
T = 50 #全局变量
def function():
    a = 10 #局部变量
    print(a)
    print(T) #可以在函数中调用全局变量。
    return a+100
print(function())
#print(a)，不能正常输出a的值，因为a是局部变量。
print(T)
```
### 读写文件
```python
# 如果没有该文件，就会新建该文件，然后写入。
text = "This is first line.\nThis is seconde line."
my_file = open("D:\_hiccup\_todo\my_file.txt","w")
my_file.write(text)
my_file.close
```

```python
# 追加写入
text = "\nThis is appended line."
my_file = open("D:\_hiccup\_todo\my_file.txt","a")
my_file.write(text)
my_file.close
```

```python
# 读取文件内容，并打印
file = open("my_file.txt","r")
content = file.read()
print(content)
```





















### 参考链接
<https://www.bilibili.com/video/BV1wW411Y7ai?from=search&seid=5616743581222647371>