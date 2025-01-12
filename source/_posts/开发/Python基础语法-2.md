---
title: Python基础语法-2
date: 2024-06-05 11:29:41
categories: 
- 开发
tags: 
- 开发
- python
top: 
---
[toc]

# 基础语法-2

## 一、文件
### 1.1、文件的编码
编码就是一种转换的规则集合，记录了内容和二进制间进行相互转换的逻辑。
编码有许多中，最常用的是`UTF-8`编码

计算机只识别0和1，需要将内容通过编码转换为0和1才能在计算机中保存，或者0和1需要通过编码转换为内容。

``` sml
内容->编码->二进制
二进制->编码->内容
```

### 1.2、文件的打开和关闭

#### 1.2.1、打开文件
语法1：`文件对象=open(name,mode,encoding)`
示例1：`f=open("D:/测试.txt","r",encoding="UTF-8")`
这种打开方式如果程序没有停止，不会自动释放文件

语法2：`with open(name,mode,encoding) as 文件对象`
通过with open() as 文件对象, 这种方式打开的文件，读取完会自动释放文件

> name:是要打开的目标文件名字符串(可以包含文件所在的具体路径)。
> mode:设置打开文件的模式(访问模式):只读，写入、追加等。
> encoding:编码格式(推荐使用UTF-8)

mode常用的三种基础访问模式：

> r：以只读方式打开文件，文件的指针将会放在文件的开头。这是默认模式
> w：打开一个文件只用于写入。如果该文件已存在则打开文件，并从头开始编辑，原有内容会被删除；如果该文件不存在，创建新文件。
> a：打开一个文件用于追加，如果文件已存在，新的内容会被写入到已有内容之后；如果该文件不存在，创建新文件进行写入

#### 1.2.2、关闭文件
- 关闭文件对象，也就是关闭对文件的占用
- 如果不调用close,同时程序没有停止运行，那么这个文件将一直被Python程序占用
- close()方法里面内置了flush()
语法：`close()`
示例:

``` python
f=open("D:/测试.txt","r",encoding="UTF-8")
f.close()
```


### 1.3、文件的读取
**读取指定长度字节**
语法：`文件对象.read(num)`
注意：不写字节(num)则读取全部内容

**读取一行**
语法：`文件对象.readlin()`

**读取全部行，得到列表**
语法：`文件对象.readlins()`
注意：读取全部行，得到列表，每一行为一个元素

**for循环文件行**
语法：`for line in 文件对象`
注意：一次循环得到一行数据


### 1.4、文件的写入
语法：`文件对象.write(内容)`
示例：

``` python
# 1.打开文件
f=open("python.txt",'w',encoding="UTF-8")
# 2.写入缓冲区
f.write("helloword")
# 3.写入到文件
f.flush()
```

注意事项：
- 直接调用write，内容并未真正写入文件，而是会积累在程序的内存中，称之为缓冲区
- 当调用flush的时候，内容会真正写入文件
- 这样做是避免频繁的操作硬盘，导致效率下降(攒一堆，一次写入磁盘)
- close()方法内置了flush功能

### 1.5、文件的追加
语法：`文件对象.write(内容)`
示例：

``` python
# 1.打开文件
f=open("python.txt",'a',encoding="UTF-8")
# 2.写入缓冲区
f.write("helloword")
# 3.写入到文件
f.flush()
```

注意事项：
- a模式，文件不存在会创建文件
- a模式，文件存在会在最后，追加写入文件


## 二、异常
当检测到`一个错误`时，Python解释器就无法继续执行了，反而出现了一些错误提示，这就是所谓的`异常`，也就是我们常说的`BUG`
### 2.1、异常的捕获方法
捕获异常的作用在于：在可能发生异常的地方，进行捕获，当异常出现的时候，提供解决方法，而不是任由其导致程序无法运行。

普通语法：

``` python
try:
	可能发生错误的代码
except:
	如果出现异常执行的代码
```

指定类型捕获：

``` python
try:
	可能发生错误的代码
except(异常类型1,异常类型2):
	如果出现指定异常执行的代码
```

捕获所有异常：

``` python
try:
	可能发生错误的代码
except Exception as e:	#as a 会把异常信息给变量a
	不论出现什么异常都执行的代码
```

异常else和异常finally：

``` python
try:
	可能发生错误的代码
except Exception as e:	#as a 会把异常信息给变量a
	不论出现什么异常都执行的代码
else:
	没有异常执行的代码
finally:
	无论是否异常都执行
```

## 三、模块和Python包
模块是一个`python文件`，以`.py结尾`，模块能定义函数，类和变量，模块里也能包含可执行代码

 pycharm快捷键：`ctrl加左键`点击模块名，就能查看.py文件
  pycharm快捷键：`ctrl加p键`点击模块名，就能查看传入参数的提示

### 3.1、模块的导入
模块在使用前需要先导入
导入语法:

``` python
[from 模块名] import [模块 | 类 | 变量 | 函数 | *] [as 别名]

```
常见的组合形式如：
``` python
import 模块名
from 模块名 import 类、变量、方法等(功能)
from 模块名 import *
import 模块名 as 别名
from 模块名 import 功能名 as 别名

```

- import 引入模块所有功能,用`模块.功能`调用
- from 模块 import 功能 单独获取一个功能,直接使用`功能`
- from可以省略，直接import即可
- as别名可以省略
- 通过"."来确定层级关系
- 模块的导入一般写在代码文件的开头

### 3.2、自定义模块并导入
定义一个.py文件作为模块，函数作为内容
示例：
``` python	
# 新建一个Python文件，命名未my_modulel.py 并定义test函数
# my_modulel.py
def test(a,b)
	print(a+b)

# 调用自定义模块
# test_my_module.py

import my_module.py
my_module.test(10,20)
```

**自定义模块中的测试(main)：**
当自定义一个模块的时候，模块里面可能需要写一些除了函数以外的测试代码，`测试模块`就是为了避免调用模块时执行这些测试代码

语法:

``` python
# my_modulel.py(自定义模块)
def test(a,b)
	print(a+b)

if __name__ == '__main__': #(在pycharm中只需要输入main，就会自动补全)
	测试语句
```



**自定义模块中的限制导入(all)**
自定义模块中如果有多个函数，improt*会把这些函数全导入过去，`__all__`就是为了做限制导入的函数
语法:

``` python
# my_modulel.py(自定义模块)
__all__ = ['test']	#限制只能improt*只能导入test函数

def test(a,b)
	print(a+b)
	
def test_b(a,b)
	print(a+b)


```

**注意事项:**
- 不同模块，同名的功能，如果都被导入，那么后导入的会覆盖先导入的
- 
### 3.3、自定义Python包
模块是一个.py文件，`python包`其实就是一个`文件夹`,在该文件夹下包含了一个`__init__.py` 文件，该文件夹可用于包含多个`模块文件`，从逻辑上看，包的本质依然是`模块`

#### 3.3.1、定义Python包
- 1.创建一个文件夹，文件夹内包含一个`__init__.py` 文件，那么这文件夹就是包(pycharm可以右键创建包)
- 2.在这个文件夹中，写入模块

#### 3.3.2、导入Python包
语法1:`from 包名 import 模块名`
语法2:`import 包名.模块名`


### 3.4、安装第三方包
在python程序生态中，有许多非常多的第三方包(非Python官方)，可以极大帮助我们提高开发效率，如：
- 科学计算中常用的: numpy包
- 数据分析中常用的：pandas包
- 大数据计算中常用的：pyspark、apache-flink包
- 图像可视化常用的：matplotlib、pyecharts包
- 人工智能常用的：tensorflow包
- 等

**安装第三方包-pip**
- 使用Python内置pip在命令提示符中输入，语法:`pip install 包名称`
- 使用国内网络下载：`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 包名称`
- pycharm中安装

## 四、json数据格式
- json是一种轻量级的数据交互格式，可以按照json指定的格式去组织和封装数据
- json本质上是一个带有特定格式的`字符串`

主要功能：json就是一种在各个变成语言中通用的数据格式，负责不同编程语言中的数据传递和交互，类似于：
- 国际通用语言-英语



  **json格式的格式:**
``` json
#json数据的格式可以是：
{"name":"admin","age":18}
 
#也可以是：
[{"name":"admin","age":18},{"name":"root","age":16},{"name":"alis","age":20}]
```

在线json网站([sojson.com](https://www.sojson.com/))

### 4.1、json格式数据转换

**Python数据和json数据的相互转换：**

``` python
#导入json模块
import json

# 准备符合格式json格式要求的python数据
data=[{"name":"admin","age":18},{"name":"root","age":16}]

#通过json.dumps(data)方法把python数据转换为json数据
data=json.dumps(data,ensure_ascii=False)	#没有中文可以不带ensure_ascii=False

#通过json.loads(data)方法把json数据转换为python数据
data=json.loads(data)
```

## 五、面向对象
面向对象编程，是许多编程语言都支持的一种编程思想。
简单理解是：基于模板(类)去创建实体(对象),使用对象完成功能开发。
面向对象的三大特性：
- 封装
- 继承
- 多态

### 5.1、类和对象
#### 5.1.1、类
- 类相当于一个定义好模板的表格，用指定的模板来存储数据
- 类有两部分组成(成员变量,成员方法)
类的定义语法：

``` python
class 类名称:
	#类中的成员变量(属性)
	name = None
	age = None
	
	#类中的成员方法(行为)
	def say_hi(self)
		print(f"Hi,我是{self.name}")	#输出:Hi,我是name
```

如果将`类`带入到现实世界无非就是分为`事和物`，事和物又细分为`属性和行为`

#### 5.1.2、类对象
类只是一种程序内的"设计图纸"，需要基于图纸生产(对象)，才能正常工作`(面向对象编程)`

类对象的定义语法:
``` python
对象=类名称()
```


### 5.2、类的方法
定义到类中的函数就叫方法
#### 5.2.1、成员方法
成员方法的定义语法：

``` python
#在类中定义方法和定义函数基本一致，但仍有细微区别:
def 方法名(self,形参1,,,,形参n):
	方法体
```

和函数区别多了一个self关键字,定义方法时候,`必须填写`的
- self表示类对象自身的意思
- 当使用类对象调用方法时，self会自动被python传入
- 在方法内部，想要访问类的成员变量，必须使用self(`self.成员变量`)

成员方法调用：

``` python
user1=Student()	#创建类对象
user1.方法名(形参1,,,,形参n)	#使用成员方法
```

#### 5.5.2、魔术方法
##### a、构造方法(__init__)
使用`__init__`方法，称之为构造方法。
- 在创建类对象(构造类)的时候,`会自动执行`。
- 在创建类对象(构造类)的时候，`将自动传递给__init__方法使用`

构造方法的定义语法：

``` python
class Student:
    age=None
    name=None
    tel=None
    def __init__(self,name,age,tel):	#构造方法定义
        self.name = name	#接收成员变量
        self.age = age		#接收成员变量
        self.tel = tel		#接收成员变量
		print("自动执行")

```

构造方法调用：

``` python
user1=Student("leo","18","123456789")	
#创建对象时直接传入成员变量，同时构造方法也会自动执行
```

##### b、字符串方法(__str__)
使用`__str__`方法，称之为字符串方法。
- 实现类对象转字符串的行为
- 可以str方法用在定制一个返回值给类对象

``` python
class Student:
    def __init__(self,name,age):	#构造方法
        self.name=name
        self.age=age
    def __str__(self):
        return (f"name:{self.name},age{self.age}")	#字符串方法，返回值给类对象

user1 = Student("leo","18")	#创建类对象，并赋值，同时将返回值给了user1
print(user1)	#输出name:leo,age18
```


### 5.3、封装

> 可以把封装描述为一种思想，将现实事物映射为程序思想

封装表示的是，将现实世界事物的：
- 属性
- 行为

封装到类中，描述为：
- 成员变量
- 成员方法

#### 5.3.1、私有成员
既然现实事物有不公开的属性和行为，那么作为现实事物在程序中映射的类，也应该支持
类中提供了两种私有成员：
- 私有成员变量
- 私有成员方法

`私有成员不能被对象调用,但是类中其它成员可以访问`

定义语法：`__变量名`和`__方法名`(两个下划线开头)
示例：

``` python
class Phone:
	IMEI=None			#序列号
	producer=None		#厂商
	
	__current_voltage=None	#当前电压(私有成员变量)
	
	def __keep_single_core(self):	#私有成员
		print("让cpu以单核模式运行以节省电量")	
	
```

> 私有成员的意义：
> 在类中提供仅内部使用的属性和方法，而不对外开放(类对象无法使用)

### 5.4、继承
继承就是一个类，继承另外一个类的成员变量和成员方法

#### 5.4.1、单继承和多继承：
**单继承:**
继承一个父类的全部内容

``` python
class 类名(父类名):
	新增类内容
```

**多继承：**
继承多个父类的全部内容
``` python
class 类名(父类1,父类2...,父类n):
	psss	#表示留空不增加内容
```

多继承注意事项：
如果父类中有同名成员方法和成员属性，先继承优先级高于后继承

#### 5.4.2、复写和调用父成员：

**复写：**
子类继承父类的成员属性和成员方法后，如对其”不满意“，可以进行复写。
语法即：`在子类中重新定义同名的属性或方法即可。`


**调用:**
在子类中调用父类成员
方式一：

> 调用父类成员
> 调用成员变量：父类名.成员变量
> 调用成员方法：父类名.成员方法(self)

方式二：

> 使用super()调用父类成员
> 调用成员变量：super().成员变量
> 调用成员方法：super.成员方法()

注意事项：只可以在子类内部调用同名的同类成员,子类的实体类调用默认是调用子类复写的

### 5.5、多态
多态，指的是：多种状态，即完成某个行为时，使用不同对象会得到不同的状态

### 5.6、类型注解
在代码中涉及数据交互的地方，提供类型的注解(显示的说明)。
主要功能：
- 帮助第三方IDE对代码进行类型推断，协助做代码提示
- 帮助开发者自身对变量进行类型注释

支持：
- 变量的类型注解
- 函数(方法)形参列表和返回值的类型注解
#### 5.6.1、变量的类型注解
基础语法：`变量:类型`

#### 5.6.2、函数(方法)的类型注解

``` Python
def 函数方法名(形参:类型,,,形参:类型)->返回值类型:
	pass
```

#### 5.6.3、Union类型 
Union可以定义联合类型注释

``` python
from typing import Union
Union[类型,...类型]
```

## 六、数据库(SQL)
### 6.1、mysql的基本使用
Windows版mysql的安装：[下载链接](https://downloads.mysql.com/archives/installer/)
图形化sql操作软件(DBeaver)：[下载链接](https://dbeaver.io/download)

**SQL语言的分类**
由于数据库管理系统(数据库软件)功能非常多，不仅仅是存储数据,还要包含：数据的管理、表的管理、库的管理、账户的管理、权限管理等。
所以，操作数据库的SQL语言，也基于功能，可以分为四类:
- 1.数据定义：DDL(Data Definition Language)
  - 库的创建删除、表的创建删除
- 2.数据操作：DML(DataManipulation Language)
   - 新增数据、删除数据、修改数据等
- 3.数据控制：DCL(Data Control Language)
   - 新增用户、删除用户、密码修改、权限管理等
- 4.数据查询：DQL(Data Query Language)
   - 基于需求查询和计算数据

**SQL的语法特征**
- SQL语法，大小写不敏感
- SQL可以单行或多行书写，最后以`;`号结束
- SQL支持注释：
   - 单行注释：-- 注释内容(-- 后面要有空格)
   - 单行注释：# 注释内容(# 后面可以不加空格，推荐加上)
   - 多行注释：/* 注释内容 */


命令行环境基础操作

``` sql
#登录
mysql -uroot -p
#查看有哪些数据库
show databases;
#使用某个数据库
use 数据库名
#查看数据内有哪些表
show tables 
#退出mysql命令行环境
exit
```

#### 6.1.1、DDL(库、表操作)
**库操作**
查看有哪些数据库
`show databases;`
使用数据库
`use 数据库名称`
创建数据库
`create database 数据库名称 charset utf8;`
删除数据库
`drop database 数据库名称;`
查看当前是使用的数据库
`select database();`

**表操作**
查看有哪些表（需要先选择数据库）
`show tables;`
删除表
`drop table 表名称;`
`drop table if exists 表名称;`
创建表

``` sql
create table 表名称(
	列名称 列类型,
	列名称 列类型
):

/*
列类型有
int					-- 整数
float				-- 浮点型
varchar(长度)		   --文本，长度为数字，做最大长度限制
date				-- 日期类型
timestamp			-- 时间戳类型
*/
```

#### 6.1.2、DML(数据操作)
DML是指数据操作语言，英文全程是Data Manipulation Language ，用来对数据库表中记录进行更新。插入`insert`   删除`delete`   更新`update`

**数据插入 insert**
基础语法：`insert into 表[(列1,列2,....列n)] values(值1,值2,....值n),(值1,值2,....值n)...,(值1,值2,....值n)`
示例:

``` sql
# 创建表
create table test_table(
	ID int,
	name varchar(20),
	age int
);

# 仅插入id列数据
insert into test_table(ID) values(10001),(10002),(10003);

# 插入全部列数据
insert into test_table(ID,name,age) values(10001,"周杰伦",31),(10002,"王力宏",33),(10003,"林俊杰",26);

# 插入全部列数据，快捷写法
insert into test_table values(10001,"周杰伦",31),(10002,"王力宏",33),(10003,"林俊杰",26);
```

**数据删除 delete**
删除行
基础语法 ：`delete from 表 [where 条件判断];`
示例：

``` sql
# 删除name为王五的数据
delete from test_table where name="王五"
# 删除ID>=10005的数据
delete from test_table where ID>=10005
```

**数据更新 update**
基础语法：`update 表 set 列=值 [where 条件判断];`
示例：

``` sql
# 修改age列的全部数据为30
update test_table set age=30
# 修改ID为10004的name为李四
update test_table set name="李四" where ID=10004
```


#### 6.1.3、DQL(数据查询)
**基础查询**
基础语法：`select 列 from 表 [where 条件判断];`
示例：

``` sql
# 查询全部数据
select * from test_table; 
# 查询id，name列中age=25的数据
select ID,name from test_table where age=25;
```

**排序分页**
排序基础语法：`select 列 from 表 [where 条件判断] order by 列 [asc|desc];`
(order by 列，以这里的列为排序对象，asc为升序，desc为降序)
分页基础语法：`select 列 from 表 [where 条件判断] limit 显示数量;`
排序分页嵌套：`select 列 from 表 [where 条件判断] order by 列 [asc|desc] limit 显示数量;`

### 6.2、pymysql模块
在python中，使用第三方库：`pymysql`来完成对mysql数据库的操作
安装：`pip install mysql`

#### 6.2.1、创建mysql数据库连接
- 创建连接对象=Connection(数据库信息)

``` python
# 创建mysql数据库连接
from pymysql import Connection  #导包
# 获取到mysql数据库的连接对象
conn = Connection(
    host='localhost',   #主机名(或ip)
    port=3306,          #端口
    user='root',        #账户名
    password='123456'   #密码
)
# 打印mysql数据库软件信息
print(conn.get_server_info())
#关闭数据库连接
conn.close()
```

#### 6.2.2、执行sql语句-查询
- 创建游标=连接对象.cursor() #创建游标对象,使用游标操作数据库，
- 游标对象.execute("执行语句")	#使用游标对象执行数据库
- 游标对象.fetchall() #接收数据以元组的形式显示

``` python
# 创建mysql数据库连接
from pymysql import Connection  #导包
# 获取到mysql数据库的连接对象
conn = Connection(
    host='localhost',   #主机名(或ip)
    port=3306,          #端口
    user='root',        #账户名
    password='123456'   #密码
)
cursor = conn.cursor()	# 创建游标对象
conn.select_db("test")	#选择数据库
cursor.execute("select * from test_table;")		#使用游标对象执行sql查询语句
results=cursor.fetchall()   #使用游标接收显示数据
print(results)				#打印数据
conn.close()				#关闭数据库连接
```

#### 6.2.3、执行sql语句-插入
- pymysql在执行数据插入或其它产生数据更改sql语句是，默认是需要确认的。
- 手动提交更改可以通过`连接对象.commit()`
- 或者使用自动提交更改，在创建连接对象中添加`autocommit=True`

示例：

``` python
# 创建mysql数据库连接
from pymysql import Connection  #导包
# 获取到mysql数据库的连接对象
conn = Connection(
    host='localhost',   #主机名(或ip)
    port=3306,          #端口
    user='root',        #账户名
    password='123456',   #密码
    autocommit=True     #自动提交更改(和连接对象.commit()效果一样)
)
cursor = conn.cursor()	# 创建游标对象
conn.select_db("test")	#选择数据库
cursor.execute("insert into test_table values(10004,'leo',21)")		#使用游标对象执行sql查询语句
#conn.commit()               #手动提交更改
conn.close()				#关闭数据库连接
```

## 七、多线程编程
- 多个进程同时在运行，即不同的程序同时运行，称之为：多任务并行执行
- 一个进程内的多个线程同时在运行，称之为：多线程并行执行

### 7.1、threading模块
python多线程可以通过`threading`内置模块来实现
语法：

``` python
import threading	#导入包
线程对象1=threading.Thread(target=函数)	#创建线程1
线程对象2=threading.Thread(target=函数,args=("函数的参数",))	#创建线程2
线程对象1.start()		#启动多线程任务
线程对象2.start()		#启动多线程任务
```
注意事项：
- 函数的参数写到args=("参数",)元组里面，组后不要忘记加`,`


示例：

``` python
#threading模块多线程示例
import time
import threading

def work(name):             #创建一个函数
    for x in range(5):
        time.sleep(1)
        print(f"我是{name},{x}")

#创建线程一
work_threa1=threading.Thread(target=work,args=("tom",))
#创建线程二
work_threa2=threading.Thread(target=work,args=("alis",))
#启动线程任务
work_threa1.start()
work_threa2.start()
```


## 八、网络编程
socket(简称：套接字)是进程之间通信的一个工具，负责进程之间网络数据传输，好比数据的搬运工
**客户端和服务端**
- 两个进程之间通过Socket进行相互通讯，就必须有服务端和客户端
- Socket服务端：等待其它进程的连接、可接受发来的消息、可以回复消息(被动)
- Socket客户端：主动连接服务端、可以发送消息、可以接收回复(主动)

### 8.1、Socket服务端编程
创建Socket服务端步骤：

``` python
# 1.创建Socket对象
import socket
socket_server = socket.socket()

# 2.绑定socket_server到指定ip和端口(元组)
socket_server.bind(("0.0.0.0",7777))

# 3. 服务端开始监听端口
## listen()里面可以填写int类型的整数，表示允许连接的数量，超出的会等待，不填的话会自动分配
socket_server.listen()

# 4.接收客户端连接，获得连接对象
conn,address = socket_server.accept()
## accept方法是一个阻塞方法，如果没有连接，会卡在这一行代码
## accept返回的是一个二元元组，用两个变量接收2个元素
## address是客户端地址,conn是消息传输对象用来发送和接收消息
print(f"接收到客户端连接，地址为{address}")

# 5.客户端连接后，通过recv方法，接收客户端发送的消息
client_data = conn.recv(1024).decode("UTF-8")
## recv方法返回值是字节,通过decode方法使用UTF-8的编码转换为字符串
## recv的传参是buffsize，缓冲区大小，一般设置为1024
print(client_data)

# 6.通过send方法回复客户端消息
conn.send("我已收到你的连接!".encode("UTF-8"))
## encode方法将字符串转换为二进制
# 7.关闭连接
conn.close()
socket_server.close()
```

### 8.1、Socket客户端编程
Socket客户端创建步骤：

``` python
# 1.创建sokcet对象
import socket
socket_client = socket.socket()
# 2.连接到服务端(ip端口为元组)
socket_client.connect(("localhost",8888))
# 3. 发送消息
socket_client.send("hello my is client".encode("UTF-8"))
# 4. 接收消息
server_data = socket_client.recv(1024).decode("UTF-8")
print(server_data)
# 5.关闭连接
socket_client.close()
```

注意事项：
- 死循环后的close方法不可执行