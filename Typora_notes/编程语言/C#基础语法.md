# C#基础语法

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

## C#常识问题

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



### 编写细节

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

### .NET平台

![image-20230308080111867](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080801939.png)

![image-20230308080311479](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080803513.png)

![image-20230308080445008](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080804082.png)

### C#学习路线

![image-20230308080654757](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080806828.png)

### 项目如何更新

> 基于面向对象编程OOP，替换DLL文件

### 面向对象的3大特性

> - 封装：隐藏内部实现细节，模块开发者之关心内部实现，模块调用者，只关心接口适用。
>   - 好处：安全性保障。（避免代码外漏）、快速应用、团队协作。
> - 继承：复用技术。
>   - 好处：一处更新，处处使用。弊端：关联会越来越复杂。
>   - 我们自己的编写的代码，一般使用继承关系的并不多。
> - 多态
>   -  概念：让一个对象的接口可以根据不同的请求，做出不同的响应。
>   -  应用：继承多态、接口多态。

> OOP开发的原则：
>
> 1. 单一职责（对象职责明确原则）
> 2. 开放封闭原则（开闭原则）
> 3. 依赖倒置原则、接口隔离原则、里氏替换原则。

### C#语法

### 变量

![image-20230308091125394](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080911454.png)

#### 变量的定义（声明）与使用

> ```C#
> namespace test1
> {
>     class Program
>     {
>         static void Main(string[] args)
>         {
>             //声明变量
>             int a;
> 
>             //赋值
>             a = 10;
> 
>             //声明的同时给赋值
>             int b = 20;
>         }
>     }
> }
> ```

#### 变量命名规范

![image-20230308092337116](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080923165.png)

### 常量

![image-20230308093518703](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080935767.png)

### 枚举

![image-20230308093910465](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080939534.png)

> ```C#
> namespace test1
> {
>     class Program
>     {
>         static void Main(string[] args)
>         {
>                 
>         }
>         public  enum Genders
>         {
>             Male,Female
>         }
> 
>     }
> }
> ```

![image-20230308152713010](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303081527068.png)

### Console类

![image-20230308153036156](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303081530194.png)

#### 格式化输出

        static void Main(string[] args)
        {
            string stuName = "zzhangsan";
            int stuAge = 10;
            Console.WriteLine("姓名：" + stuName + "年龄" +stuAge);
            Console.WriteLine("姓名：{0} 年龄：{1}" ,stuName,stuAge);
            Console.ReadLine();
        }

#### 制表符（数据库会用）

```C#
namespace test1
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("姓名\t年龄\t班级\t");
            Console.WriteLine("张三\t18\t21班\t");
            Console.WriteLine("李四\t19\t22班\t");
            Console.WriteLine("姓王五\t20\t23班\t");
            Console.ReadLine();
        }
    }
}

```

### 自动类型转换

![image-20230308160311746](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303081603806.png)

![image-20230308165548122](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303081655187.png)

![image-20230308195928586](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303081959641.png)

#### Parse和Convert

![image-20230308200111584](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082001634.png)

![image-20230308200427697](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082004746.png)

### 运算符

![image-20230308200722087](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082007131.png)

### 分支结构

#### switch和多重if的比较

![image-20230308204255520](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082042569.png)

### 循环结构

![image-20230308205140275](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082051324.png)

### 数据类型

![image-20230308091229109](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303080912174.png)

### 字符型存储

![image-20230309103346903](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303091033948.png)

![image-20230309103410091](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303091034215.png)

### 字符串处理

#### IndexOf方法

![image-20230308210714992](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082107029.png)

#### Length属性

![image-20230308210741140](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082107179.png)

#### Equals方法

![image-20230308210807551](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082108597.png)

#### Substring方法

![image-20230308212028024](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082120088.png)

#### Format方法

![image-20230308211732612](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082117689.png)

![image-20230308231140603](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082311648.png)

![image-20230308231443656](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082314715.png)

![image-20230308232027247](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082320305.png)

#### Trim方法

![image-20230308233452114](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082334151.png)

#### 转换大小写

![image-20230308233513027](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082335063.png)

#### 找最后一个字符串索引

![image-20230308233545070](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082335107.png)

#### 字符串分离和链接

![image-20230309001539770](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303090015833.png)

#### StringBuilder类定义

![image-20230308234815206](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082348280.png)

### 数组

![image-20230308235624399](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082356457.png)

![image-20230308235652048](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082356120.png)

![image-20230309095315812](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303090953892.png)

### 引用类型

![image-20230309095814871](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303090958911.png)

### 遍历

![image-20230309001024762](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303090010819.png)

