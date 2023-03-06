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
- 
