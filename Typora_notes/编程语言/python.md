# python

[TOC]

> python基础课：
>
> 1. [黑马程序员python教程](https://www.bilibili.com/video/BV1qW4y1a7fU?p=1&vd_source=91ddf1aeb53bd3336e78168da8d0b7dd)
>
> 环境搭建参考：
>
> 1. [Anaconda安装+PyCharm安装和基本使用](https://www.bilibili.com/video/BV1Vu411Y7gL/?spm_id_from=333.337.top_right_bar_window_history.content.click&vd_source=91ddf1aeb53bd3336e78168da8d0b7dd)
>
> 2. [anaconda镜像 Index of / (anaconda.com)](https://repo.anaconda.com/archive/)
> 3. [python3.10.4](https://www.python.org/downloads/windows/)

## 初识python

- python前世今生
  - 1989吉多范罗苏姆在圣诞节开发了一款解释器程序，python雏形诞生
  - 1991第一个python解释器程序诞生
  - python出自Monty Python‘s Flying Circus，标志为两条蟒蛇

- python解释器

  - 计算机只认识01二进制
  - 解释器作用
    - 将python代码翻译成01二进制
    - 将二进制提交给计算机去执行

  - .py后缀是python的代码文件
  - python解释器程序是python.exe

- 根据执行方式不同，编程语言分为两类

  - 静态语言：使用编译执行的编程语言c/c++，java
  - 脚本语言：使用解释执行的编程语言pthon，javascript，php

- 两种编程方式
  - 交互式，在解释器程序下一条条执行代码
  - 文件式，例如在cmd下执行一批文件

  ```cmd
  python test.py
  ```

  



### 缩进

- 严格明确：缩进是语法的一部分
- 所属关系：表达代码间层次关系
- 长度一致：4个空格 或 1个tab

### 注释

```python
#	单行注释 

'''
     单引号
     多行注释
'''

"""
	双引号
	多行注释
"""
```

### 变量

用来保存和表示数据的占位符号

## 变量类型

​	![image-20240222225343876](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402222253010.png)



> 测试类型

```
price = 100
type(price)

==>
<class 'int'>
```

> 判断类型

```
price = 100
isinstance(price,int)

==>
True
```



### 命名

变量采用标识符来表示，==关联标识符==的过程叫命名

- 命名规则
  - 大小写字母、数字、下划线、汉字

- 注意事项
  - 大小写敏感
  - 首字符不能是数字
  - 不能与保留字相同

- 保留字

```
import keyword
keyword,kwlist

==>
[关键字列表]
```

![image-20230103152204438](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230103152204438.png)



## 输出函数print

> 语法

```python
print(*objects, sep=' ',end='\n',file=sys.stdout,flush=False)
```

> 案例

```
# 将默认的空格分隔符换成 ,
print('hello','world',sep=',')

# 将默认的换行符换成 ,
print('hello','world',end=',')

# 输出到文件
file_source = open('test.txt','W')
print('hello','world',file=ile_source)
file_source.close()
```



## 输出函数input

> 语法

```python
price = input(' price = ')
number = input(' number = ')
# 下面这句会报错，因为input默认输入的是str类型
print(' all need = ', price * number)

# 修改方法
print(' all need = ', int(price) * int(number) )
```



## 运算符

### 简单运算符

> 简单运算符：
>
> - 加法
>
>   ```python
>   num1 = 1314
>   num2 = 520
>   print(num1 + num2)	# 打印 1314520
>   ```
>
>   
>
> - 乘法
>
>   ```python
>   pirnt('=' * 5)	# 打印 5个=
>   ```
>
>   
>
> - 除法
>
>   ```python
>   a = 10
>   b = 0
>   pirnt(a / b)	# 除数不能为0
>   ```
>
>   
>
> - 向下取整
>
>   ```python
>   a = 10
>   b =3
>   print(a / b)	# 打印 3.333
>   print(a // b)	# 打印 3
>   ```
>
>   
>
> - 余数
>
>   ```python
>   print(10/3)	# 3.333
>   print(10%3)	# 1
>     
>   print(3/10) # 0.3
>   print(3%10) # 3
>     
>   print(-10%3) # r = -10 - 3 * (-10 // 3) = 2
>   ```
>
>   
>
> - 赋值
>
>   ```python
>   a, b = 5 , 10
>   print(a, b) # 5 10
>     
>   # a,b 快速交换
>   a, b = b, a 
>   ```

### 比较运算符

> 注意 False 、 True 首字母大写

### 逻辑运算符

```python
print(1 and 0)				# 打印 0
print(1 and 0 and 'abc')	# 打印 0 ，哪里False就输出哪里
print(1 and 0.0 and 'abc')	# 打印0.0，哪里False就输出哪里

print(0 or 100)				# 打印100,哪里True就输出哪里
print(9 or 10 or 100)		# 打印9,哪里True就输出哪里
print(0 or '' or 100)		# 打印100

# or 高端操作，可以用来简化 if else的判断逻辑
```



## 流程控制结构

> 1. 顺序
>
> 2. 条件
>
>    ```python
>    grade = False
>    if grade:
>        print('pass')
>    else:
>        print('not pass')
>    ```
>
>    
>
> 3. 循环



!!! 看到P38



#### 数据类型

- 字符串

  - 由一对单引号或一对双引号

  - 字符串是==有序序列==，序号从0开始

    - 正向递增序号

    - 反向递减序号

    ![image-20230103153034331](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230103153034331.png)

  - 字符串的使用

    - 索引

  ```python
  TempStr[-1]
  ```

  - ​	切片

  ```python
  TempStr[0:-1]		//从序号0开始，到最后第二个字符
  ```

- 数字类型

  - 整数
  - 浮点数

- 列表类型

由0个或多个数据组成的有序序列



## 语法

### 字面量

代码中，被写在代码中的固定的值，成为字面量

- 常用的值类型

![image-20230821005801078](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308210058234.png)

### 注释

规范：在#和注释内容之间，要间隔一个空格

- 单行注释
  - 对单行代码进行注释
  - 一小段代码

```python
# 我是单行注释
```

- 多行注释
  - 整个python代码文件
  - 类
  - 方法

```py
"""
我是多行注释
我是多行注释
我是多行注释
"""
```

### 变量

在程序运行时，能存储计算结果或能表示值的抽象概念

### 数据类型

![image-20230821192758724](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308211927872.png)

- 验证字面量的数据类型

![image-20230821192934439](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308211929477.png)

- 验证变量的数据类型

![image-20230821193916364](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308211939431.png)

### 类型转换

![image-20230821200024142](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308212000204.png)

- 所有类型都能转到str
- 数字类型转换要考虑精度

### 标识符

大小写敏感，区分大小写

- 标识符命名中，只允许
  - 英文
  - 中文（不推荐）
  - 数字（不可以在开头）
  - 下划线 _
- 标识符命名中，不可使用关键字

![image-20230821230643340](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308212306399.png)

- 标识符规范
  - 变量
    - 见名知意
    - 多个单词组合变量名，使用下划线做分隔
    - 英文字母全小写
  - 类
  - 方法



### 运算符

- 算术运算符

![image-20230821231126316](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308212311378.png)

- 赋值运算符

![image-20230821231454472](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308212314523.png)

- 复合赋值运算符

![image-20230821231538600](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308212315685.png)

### 字符串扩展

#### 字符串的三种定义方式

1. 单引号定义法

```py
name = 'hello'
```

2. 双引号定义法

```python
name = "hello"
```

3. 三引号定义法

多行注释用一个变量接收，就变成了三引号定义的字符串

```py
name = """hello"""
```

- 如何定义包含引号的字符串
  - 单引号定义法，可与包含双引号
  - 双引号定义法，可以包含单引号
  - 可以用转义字符（ \ ）来解除引号效果
