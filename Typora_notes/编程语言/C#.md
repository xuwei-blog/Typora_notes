# C#

## 概述

[TOC]

### 上位机开发

![image-20230306145230584](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303061452680.png)

![image-20230306145457383](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303061454439.png)

### 语法入门

### IDE操作

#### 新建项目

> 文件 - 新建项目
>
> 1. 版本的选择：建议选4或者4.6
>
> 2. 选择开发语言：一般都是C#
> 3. 项目类型：初学用控制台
> 4. 项目名称：要有意义
> 5. 位置：项目的位置
> 6. 解决方案名称：默认和项目名称一样

#### 解决方案

> 一个解决方案，可以添加若干个项目

#### 项目结构

![image-20230306174623407](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303061746568.png)

- Properties文件夹：属性文件夹
  - AssemblyInfo.cs文件：里面的配置信息主要是用来保存项目的版权信息
- Program.cs文件：是项目的启动入口文件
- 引用：我们当前项目所需的.NET底层模块
  - 后续可以添加
- 剩下的是我们自己添加的其他类文件

### 代码编辑区域的说明

- 命名空间
  - 关键字：using
  - 引用之后，可以使用该引用下的类
  - 如果不using命名空间，使用类的时候，需要 命名空间.类名

![image-20230306180501592](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303061805192.png)

- 项目的命名空间
  - 默认和项目名称一样
  - 一个类必须包括在一个命名空间里
  - class是一个程序的基本单元
  - mian程序的入口方法

![image-20230306180613032](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303061806058.png)

### 代码规范

- 在C#中严格区分大小写
- 每条语句写完后，要用英文半角分号结尾（;）

### .NET程序编译和运行过程

![image-20230307225510454](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303072339620.png)

#### MSIL查看工具（IL DASM）

![image-20230307230106951](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303072339555.png)

#### 文件类型

- exe文件
  - 可执行文件，里面是IL指令
- dll文件
  - 动态链接库文件，里面是IL指令
- pdb文件
  - Program Debug DataBase 程序调试数据库文件
  - 调试的时候定位源码，方便调试

- vshost文件
  - 用于提交调试效率的宿主进程
  - vs调试的时候，打开的是这个文件
  - 可以让VS跟踪调试信息

- manifest文件
  - 是一个XML文件，用于COM类，接口库的绑定和激活
  - 无需写程序的注册表

- config
  - 项目的配置文件

## C#语法

### Main方法

> 作用：程序入口方法
>
> 要求：一个程序只有一个Main()方法，首字母要大写、返回值为void或者int、命令行参数是可选的

> 4种形式：
>
> ```C#
> static void Main(string[] args){ }
> 
> static int Main(string[] args){ }
> 
> static void Main(){ }
> 
> static int Main(){ }
> ```

### 注释

> 作用：说明代码的作用，注释不参与编译

> 单行注释
>
> 多行注释：对类进行说明
>
> ```C#
> /*
>  
> */
> ```
>
> 文档注释：对函数进行说明
>
> ```C#
> ///
> ```

### 代码折叠器region

> 作用：将多行代码折叠，使得代码可读性增强，容易查询。
>
> 要求：必须成对出现。

![image-20230307233020243](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303072338086.png)

> 如何使用：
>
> ```C#
> #region	这是一个说明
>    //代码...
> #endregion
> ```



### 编写问题小节

- 程序语句：

  大小写：C#严格区分大小写，比如Class和class是完全不一样的。

  位置：类必须在指定的命名空间中，方法、属性、字段的定义，必须放到类中。

- 引号

  使用双引号""，要求英文半角，并且成对出现。

  字符串的定义必须使用双引号。

  带空格的字符串"  "和不带空格的字符串""是完全不一样的。

- 注释

  关键性的语句需要添加注释。

  类名称前应该使用多行注释（文档注释），说明类的功能和使用方法。

  复杂方法前面应该使用文档注释，说明方法的功能，参数的含义，返回值信息等。

  文档注释一方面给我们开发者日后做参考，还有就是给调用者提供智能提示。
