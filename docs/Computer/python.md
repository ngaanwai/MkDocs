---
title: python
tags: [computer]
---

## 安装
## 语法
### Strings 字符串
用引号包起来
Python中单引号'和双引号"没区别  
用三个单引号'''或三个双引号"""可以直接print多行字符串而不必使用\转义符  
字符串可以用+连接，用*重复
字符串后面用[]实现切片功能
```python
print('''Hello World!
'''*3)
```
```console
Hello World!
Hello World!
Hello World!
```
```python
print('''Hello
'''+input('''what's your name?''') )
```
```console
what's your name?yanwei
Hello
yanwei
```

#### len(string)  
get the length of the string 获得字符串长度 
```python
print(len(input('''What's your name?''')))
```
```console
What's your name?yanwei
6
```

### Variables 变量
下面的内容效果很上面的一样
``` python
name = input('''what's your name?''')
length = len(name)
print(length)
```
### Numbers
#### Integer

#### Float
##### round(float,n)  
n代表小数点后面的位数

### Booleans


### Arithmetic Operators
|Operator|Name|
|---|---|
|+|Addition|
|-|Subtraction|
|/|Divsion|
|%|Modulus|
|**|Exponentiation|
|//|Floor division|

### F Strings
以f或F开头 ，用{}把变量包起来
```python
person = {'name':'yanwei','age':20}
print(f"The person is {person['name'].title()},aged {person['age']}.")
```
```console
The person is Yanwei,aged 20.
```

### if_else
```python
a = int(input("输入整数a的值"))
b = int(input("输入整数b的值"))
if b > a:
  print("b is greater than a")
else:
  print("b is not greater than a")
```

### Comparison Operators
|Operator|Meaning|
|---|---|
|>|Greater than|
|<|Less than|
|>=|Greater than equal to|
|<=|Less than equal to|

### Logical Operators
and
or
not

### Lists
#### list.index()
Returns the index of the first element with the specified value
```python
fruits = ['apple','banana','cheery']
print(fruits.index('cheery'))
```
```console
2
```
### for loop with lists
```python
fruits = ["apple", "banana", "cherry"]
for x in fruits:
  print(x)
```
```console
apple
banana
cherry
```
### while loop 
```python
i = 1
while i < 6:
  print(i)
  i += 1
```
```console
1
2
3
4
5
```
### Functions
```python
def my_function(something):
  #Do this with something
  #Then do this
```
```python
my_function(123)
```
something is parameter
123 is argument
The parameter is the name of the data that's being passed in ,The argument is the actual value of the data.


### Virtual Environment 虚拟环境
新建虚拟环境  
```
python -m venv /path/to/new/virtual/environment
```
激活虚拟环境  
```
source /path/to/new/virtual/environment/bin/activate
```



# reference
https://docs.python.org/