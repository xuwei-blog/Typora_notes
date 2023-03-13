

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

## C#语法

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

#### 变量的类型

- 值类型（Value types）
- 引用类型（Reference types）
- 指针类型（Pointer types）

#### 值类型（Value types）

| 类型    | 描述                                 | 范围                                                    | 默认值 |
| :------ | :----------------------------------- | :------------------------------------------------------ | :----- |
| bool    | 布尔值                               | True 或 False                                           | False  |
| byte    | 8 位无符号整数                       | 0 到 255                                                | 0      |
| char    | 16 位 Unicode 字符                   | U +0000 到 U +ffff                                      | '\0'   |
| decimal | 128 位精确的十进制值，28-29 有效位数 | (-7.9 x 1028 到 7.9 x 1028) / 100 到 28                 | 0.0M   |
| double  | 64 位双精度浮点型                    | (+/-)5.0 x 10-324 到 (+/-)1.7 x 10308                   | 0.0D   |
| float   | 32 位单精度浮点型                    | -3.4 x 1038 到 + 3.4 x 1038                             | 0.0F   |
| int     | 32 位有符号整数类型                  | -2,147,483,648 到 2,147,483,647                         | 0      |
| long    | 64 位有符号整数类型                  | -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 | 0L     |
| sbyte   | 8 位有符号整数类型                   | -128 到 127                                             | 0      |
| short   | 16 位有符号整数类型                  | -32,768 到 32,767                                       | 0      |
| uint    | 32 位无符号整数类型                  | 0 到 4,294,967,295                                      | 0      |
| ulong   | 64 位无符号整数类型                  | 0 到 18,446,744,073,709,551,615                         | 0      |
| ushort  | 16 位无符号整数类型                  | 0 到 65,535                                             | 0      |

#### 引用类型（Reference types）

>  引用类型不包含存储在变量中的实际数据，但它们包含对变量的引用
>
> 引用类型的数据是一个内存位置
>
> 使用多个变量时，引用类型可以指向一个内存位置
>
> 如果内存位置的数据是由一个变量改变的，其他变量会自动反映这种值的变化
>
> **内置的** 引用类型有：**object**、**dynamic** 和 **string**

##### 对象（Object）类型

> **对象（Object）类型** 是 C# 通用类型系统（Common Type System - CTS）中所有数据类型的终极基类
>
> Object 是 System.Object 类的别名
>
> 对象（Object）类型可以被分配任何其他类型（值类型、引用类型、预定义类型或用户自定义类型）的值
>
> 但在分配值之前，需要先进行类型转换。

>  当一个值类型转换为对象类型时，则被称为 **装箱**；另一方面，当一个对象类型转换为值类型时，则被称为 **拆箱**。

```C#
object obj;
obj = 100; // 这是装箱
```

##### 动态（Dynamic）类型

> 可以存储任何类型的值在动态数据类型变量中
>
> 动态数据类型变量的类型检查是在运行时发生的
>
> 动态类型与对象类型相似，但是对象类型变量的类型检查是在编译时发生的，而动态类型变量的类型检查是在运行时发生的

##### 字符串（String）类型

> **字符串（String）类型** 允许给变量分配任何字符串值。
>
> 字符串（String）类型是 System.String 类的别名。
>
> 它是从对象（Object）类型派生的。
>
> 字符串（String）类型的值可以通过两种形式进行分配：引号和 @引号。

```C#
String str = "D:\\table";
String str = @"D:\table";	//两句代码等价
```



#### 指针类型（Pointer types）

> 指针类型变量存储另一种类型的内存地址



#### 关键字

- 保留关键字

|           |           |          |            |                        |                       |         |
| --------- | --------- | -------- | ---------- | ---------------------- | --------------------- | ------- |
| abstract  | as        | base     | bool       | break                  | byte                  | case    |
| catch     | char      | checked  | class      | const                  | continue              | decimal |
| default   | delegate  | do       | double     | else                   | enum                  | event   |
| explicit  | extern    | false    | finally    | fixed                  | float                 | for     |
| foreach   | goto      | if       | implicit   | in                     | in (generic modifier) | int     |
| interface | internal  | is       | lock       | long                   | namespace             | new     |
| null      | object    | operator | out        | out (generic modifier) | override              | params  |
| private   | protected | public   | readonly   | ref                    | return                | sbyte   |
| sealed    | short     | sizeof   | stackalloc | static                 | string                | struct  |
| switch    | this      | throw    | true       | try                    | typeof                | uint    |
| ulong     | unchecked | unsafe   | ushort     | using                  | virtual               | void    |
| volatile  | while     |          |            |                        |                       |         |

- 上下文关键字

|                  |        |           |            |         |         |                |
| ---------------- | ------ | --------- | ---------- | ------- | ------- | -------------- |
| add              | alias  | ascending | descending | dynamic | from    | get            |
| global           | group  | into      | join       | let     | orderby | partial (type) |
| partial (method) | remove | select    | set        |         |         |                |

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

#### 隐式类型转换

```MARKDOWN
隐式转换是指将一个较小范围的数据类型转换为较大范围的数据类型时，编译器会自动完成类型转换，这些转换是 C# 默认的以安全方式进行的转换, 不会导致数据丢失。

例如，从小的整数类型转换为大的整数类型，从派生类转换为基类。将一个 byte 类型的变量赋值给 int 类型的变量，编译器会自动将 byte 类型转换为 int 类型，不需要显示转换。
```

#### 强制类型转换（显示转换）

```markdown
显式转换是指将一个较大范围的数据类型转换为较小范围的数据类型时，或者将一个对象类型转换为另一个对象类型时，需要使用强制类型转换符号进行显示转换，强制转换会造成数据丢失。
```

#### 拆箱和装箱

![image-20230313232007647](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303132320719.png)

#### 强制类型转换内置方法

| 序号 | 方法 & 描述                                                  |
| :--: | :----------------------------------------------------------- |
|  1   | **ToBoolean** 如果可能的话，把类型转换为布尔型。             |
|  2   | **ToByte** 把类型转换为字节类型。                            |
|  3   | **ToChar** 如果可能的话，把类型转换为单个 Unicode 字符类型。 |
|  4   | **ToDateTime** 把类型（整数或字符串类型）转换为 日期-时间 结构。 |
|  5   | **ToDecimal** 把浮点型或整数类型转换为十进制类型。           |
|  6   | **ToDouble** 把类型转换为双精度浮点型。                      |
|  7   | **ToInt16** 把类型转换为 16 位整数类型。                     |
|  8   | **ToInt32** 把类型转换为 32 位整数类型。                     |
|  9   | **ToInt64** 把类型转换为 64 位整数类型。                     |
|  10  | **ToSbyte** 把类型转换为有符号字节类型。                     |
|  11  | **ToSingle** 把类型转换为小浮点数类型。                      |
|  12  | **ToString** 把类型转换为字符串类型。                        |
|  13  | **ToType** 把类型转换为指定类型。                            |
|  14  | **ToUInt16** 把类型转换为 16 位无符号整数类型。              |
|  15  | **ToUInt32** 把类型转换为 32 位无符号整数类型。              |
|  16  | **ToUInt64** 把类型转换为 64 位无符号整数类型。              |



#### Parse和Convert

![image-20230308195928586](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303101013013.png)

![image-20230308200111584](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082001634.png)

![image-20230308200427697](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082004746.png)

### 运算符

> **优先级简易概括**：有括号先括号，后乘除在加减，然后位移再关系，逻辑完后条件，最后一个逗号

#### 运算符优先级

| 类别       | 运算符                            | 结合性   |
| :--------- | :-------------------------------- | :------- |
| 后缀       | () [] -> . ++ - -                 | 从左到右 |
| 一元       | + - ! ~ ++ - - (type)* & sizeof   | 从右到左 |
| 乘除       | * / %                             | 从左到右 |
| 加减       | + -                               | 从左到右 |
| 移位       | << >>                             | 从左到右 |
| 关系       | < <= > >=                         | 从左到右 |
| 相等       | == !=                             | 从左到右 |
| 位与 AND   | &                                 | 从左到右 |
| 位异或 XOR | ^                                 | 从左到右 |
| 位或 OR    | \|                                | 从左到右 |
| 逻辑与 AND | &&                                | 从左到右 |
| 逻辑或 OR  | \|\|                              | 从左到右 |
| 条件       | ?:                                | 从右到左 |
| 赋值       | = += -= *= /= %=>>= <<= &= ^= \|= | 从右到左 |
| 逗号       | ,                                 | 从左到右 |

#### 算术运算符

| 类别       | 运算符                            | 结合性   |
| :--------- | :-------------------------------- | :------- |
| 后缀       | () [] -> . ++ - -                 | 从左到右 |
| 一元       | + - ! ~ ++ - - (type)* & sizeof   | 从右到左 |
| 乘除       | * / %                             | 从左到右 |
| 加减       | + -                               | 从左到右 |
| 移位       | << >>                             | 从左到右 |
| 关系       | < <= > >=                         | 从左到右 |
| 相等       | == !=                             | 从左到右 |
| 位与 AND   | &                                 | 从左到右 |
| 位异或 XOR | ^                                 | 从左到右 |
| 位或 OR    | \|                                | 从左到右 |
| 逻辑与 AND | &&                                | 从左到右 |
| 逻辑或 OR  | \|\|                              | 从左到右 |
| 条件       | ?:                                | 从右到左 |
| 赋值       | = += -= *= /= %=>>= <<= &= ^= \|= | 从右到左 |
| 逗号       | ,                                 | 从左到右 |

#### 关系运算符

| 运算符 | 描述                                                         | 实例              |
| :----- | :----------------------------------------------------------- | :---------------- |
| ==     | 检查两个操作数的值是否相等，如果相等则条件为真。             | (A == B) 不为真。 |
| !=     | 检查两个操作数的值是否相等，如果不相等则条件为真。           | (A != B) 为真。   |
| >      | 检查左操作数的值是否大于右操作数的值，如果是则条件为真。     | (A > B) 不为真。  |
| <      | 检查左操作数的值是否小于右操作数的值，如果是则条件为真。     | (A < B) 为真。    |
| >=     | 检查左操作数的值是否大于或等于右操作数的值，如果是则条件为真。 | (A >= B) 不为真。 |
| <=     | 检查左操作数的值是否小于或等于右操作数的值，如果是则条件为真。 | (A <= B) 为真。   |

#### 逻辑运算符

| 运算符 | 描述                                                         | 实例              |
| :----- | :----------------------------------------------------------- | :---------------- |
| &&     | 称为逻辑与运算符。如果两个操作数都非零，则条件为真。         | (A && B) 为假。   |
| \|\|   | 称为逻辑或运算符。如果两个操作数中有任意一个非零，则条件为真。 | (A \|\| B) 为真。 |
| !      | 称为逻辑非运算符。用来逆转操作数的逻辑状态。如果条件为真则逻辑非运算符将使其为假。 | !(A && B) 为真。  |

#### 位运算符

| 运算符 | 描述                                                         | 实例                                                         |
| :----- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| &      | 如果同时存在于两个操作数中，二进制 AND 运算符复制一位到结果中。 | (A & B) 将得到 12，即为 0000 1100                            |
| \|     | 如果存在于任一操作数中，二进制 OR 运算符复制一位到结果中。   | (A \| B) 将得到 61，即为 0011 1101                           |
| ^      | 如果存在于其中一个操作数中但不同时存在于两个操作数中，二进制异或运算符复制一位到结果中。 | (A ^ B) 将得到 49，即为 0011 0001                            |
| ~      | 按位取反运算符是一元运算符，具有"翻转"位效果，即0变成1，1变成0，包括符号位。 | (~A ) 将得到 -61，即为 1100 0011，一个有符号二进制数的补码形式。 |
| <<     | 二进制左移运算符。左操作数的值向左移动右操作数指定的位数。   | A << 2 将得到 240，即为 1111 0000                            |
| >>     | 二进制右移运算符。左操作数的值向右移动右操作数指定的位数。   | A >> 2 将得到 15，即为 0000 1111                             |

| p    | q    | p & q | p \| q | p ^ q |
| :--- | :--- | :---- | :----- | :---- |
| 0    | 0    | 0     | 0      | 0     |
| 0    | 1    | 0     | 1      | 1     |
| 1    | 1    | 1     | 1      | 0     |
| 1    | 0    | 0     | 1      | 1     |

#### 赋值运算符

| 运算符 | 描述                                                         | 实例                            |
| :----- | :----------------------------------------------------------- | :------------------------------ |
| =      | 简单的赋值运算符，把右边操作数的值赋给左边操作数             | C = A + B 将把 A + B 的值赋给 C |
| +=     | 加且赋值运算符，把右边操作数加上左边操作数的结果赋值给左边操作数 | C += A 相当于 C = C + A         |
| -=     | 减且赋值运算符，把左边操作数减去右边操作数的结果赋值给左边操作数 | C -= A 相当于 C = C - A         |
| *=     | 乘且赋值运算符，把右边操作数乘以左边操作数的结果赋值给左边操作数 | C *= A 相当于 C = C * A         |
| /=     | 除且赋值运算符，把左边操作数除以右边操作数的结果赋值给左边操作数 | C /= A 相当于 C = C / A         |
| %=     | 求模且赋值运算符，求两个操作数的模赋值给左边操作数           | C %= A 相当于 C = C % A         |
| <<=    | 左移且赋值运算符                                             | C <<= 2 等同于 C = C << 2       |
| >>=    | 右移且赋值运算符                                             | C >>= 2 等同于 C = C >> 2       |
| &=     | 按位与且赋值运算符                                           | C &= 2 等同于 C = C & 2         |
| ^=     | 按位异或且赋值运算符                                         | C ^= 2 等同于 C = C ^ 2         |
| \|=    | 按位或且赋值运算符                                           | C \|= 2 等同于 C = C \| 2       |

#### 其他运算符

| 运算符   | 描述                                   | 实例                                                         |
| :------- | :------------------------------------- | :----------------------------------------------------------- |
| sizeof() | 返回数据类型的大小。                   | sizeof(int)，将返回 4.                                       |
| typeof() | 返回 class 的类型。                    | typeof(StreamReader);                                        |
| &        | 返回变量的地址。                       | &a; 将得到变量的实际地址。                                   |
| *        | 变量的指针。                           | *a; 将指向一个变量。                                         |
| ? :      | 条件表达式                             | 如果条件为真 ? 则为 X : 否则为 Y                             |
| is       | 判断对象是否为某一类型。               | If( Ford is Car) // 检查 Ford 是否是 Car 类的一个对象。      |
| as       | 强制转换，即使转换失败也不会抛出异常。 | Object obj = new StringReader("Hello"); StringReader r = obj as StringReader; |

### 分支结构

#### 判断语句

| 语句             | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| if 语句          | 一个 **if 语句** 由一个布尔表达式后跟一个或多个语句组成。    |
| if...else 语句   | 一个 **if 语句** 后可跟一个可选的 **else 语句**，else 语句在布尔表达式为假时执行。 |
| 嵌套 if 语句     | 您可以在一个 **if** 或 **else if** 语句内使用另一个 **if** 或 **else if** 语句。 |
| switch 语句      | 一个 **switch** 语句允许测试一个变量等于多个值时的情况。     |
| 嵌套 switch 语句 | 您可以在一个 **switch** 语句内使用另一个 **switch** 语句。   |

#### switch和多重if的比较

![image-20230308204255520](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082042569.png)

### 循环结构

| 循环类型         | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| while 循环       | 当给定条件为真时，重复语句或语句组。它会在执行循环主体之前测试条件。 |
| for/foreach 循环 | 多次执行一个语句序列，简化管理循环变量的代码。               |
| do...while 循环  | 除了它是在循环主体结尾测试条件外，其他与 while 语句类似。    |
| 嵌套循环         | 您可以在 while、for 或 do..while 循环内使用一个或多个循环。  |

![image-20230308205140275](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303082051324.png)

#### 循环控制语句

| 控制语句      | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| break 语句    | 终止 **loop** 或 **switch** 语句，程序流将继续执行紧接着 loop 或 switch 的下一条语句。 |
| continue 语句 | 跳过本轮循环，开始下一轮循环。                               |

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



### 遍历

![image-20230309001024762](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303090010819.png)

