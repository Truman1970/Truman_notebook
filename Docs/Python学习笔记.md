环境：3.x版本  
> 3.x和2.x区别？
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