---
title: Python常用函数使用
date: 2024-05-20 16:30:02
categories: 
- 开发
tags: 
- python
- 函数
- 开发
top: 
---
[toc]

## 1、print---输出内容
 **输出不换行**
加上and=''
``` python
print("hello",and='')
print("word",and='')
```
## 2、len---统计字符串长度
用来统计字符串长度

``` python
name = "tanglx"
print(f"长度为：{len(name)}")
```

## 3. type---识别变量类型
打印识别变量类型

例题：
``` routeros
name='汤龙祥'
Age=18
Height=1.75
print(type(name))
print(type(Age))
print(type(Height))
```

## 4. range---获得一个数字序列
range语句的功能是：
- 获得一个数字序列

语法：
语法1：

``` maxima
range(num)
# 从0开始，到num结束(不含num本身)
```

语法2：

``` stylus
range(num1,num2)
# 从num1开始，到num2结束(不含num2本身)
```

语法3：

``` maxima
range(num1,num2,step)
# 从num1开始，到num2结束,step为步长
```