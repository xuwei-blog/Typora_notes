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

  

### 程序格式框架

#### 缩进

- 严格明确：缩进是语法的一部分
- 所属关系：表达代码间层次关系
- 长度一致：4个空格 或 1个tab

#### 注释

```python
#单行注释 

'''
多行注释
第二行注释
'''
```

#### 变量

用来保存和表示数据的占位符号

#### 命名

变量采用标识符来表示，==关联标识符==的过程叫命名

- 命名规则
  - 大小写字母、数字、下划线、汉字

- 注意事项
  - 大小写敏感
  - 首字符不能是数字
  - 不能与保留字相同

- 保留字

![image-20230103152204438](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230103152204438.png)

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
