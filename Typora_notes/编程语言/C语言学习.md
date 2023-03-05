# C语言学习

## 概述

[TOC]

## C语言概述

### C语言应用范围

![image-20230115234625783](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230115234625783.png)

### 32个关键字

![image-20230124153026379](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230124153026379.png)

### 9个控制语句

![image-20230116000330057](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230116000330057.png)

### 34种运算符

![image-20230116000455808](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230116000455808.png)

### gcc

- （GNU Compiler Collection，GNU 编译器套件），是由 GNU 开发的编程语言编译器

- gcc原本作为GNU操作系统的官方编译器，现已被大多数类Unix操作系统（如Linux、BSD、Mac OS X等）采纳为标准的编译器，gcc同样适用于微软的Windows。

- gcc4步：预处理、编译、汇编、链接

![image-20230124144149137](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230124144149137.png)

1. 预处理

```cmd
gcc -E xxx.c -o xxx.i
```

- 头文件展开（不检查语法）
- 宏定义替换（宏名替换宏值）
- 替换注释（变成空行）
- 展开条件编译 （根据条件展开指令）

```c
#define X 1
#ifdef X
printf（“666”）；
#endif
```



2. 编译

```cmd
gcc -S xxx.i -o xxx.s
```

- 逐行检查语法错误（==最耗时的过程==）
- 将C程序翻译成汇编指令，得到 .s 的汇编文件



3. 汇编

```c
gcc -c xxx.s -o xxx.o
```

- 将汇编指令翻译成 二进制编码



4. 链接

```c
gcc xxx.o -o xxx.exe
```

- 数据段合并
- 数据地址回填
- 库引入



### 寄存器

CPU总线是64位，寄存器也是64位，向下兼容32位。

在64位的CPU架构上运行64位操作系统，称系统是64位

在64位的CPU架构上运行32位操作系统，称系统是32位

- 寄存器名字

![image-20230124151609670](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230124151609670.png)



### 注释

单行注释：//

多行注释： /* 注释内容 */



### 函数

- system函数：pause、cmd、mspain、calc、notepad、cls

```C
system("pasue");
```



### C与语言嵌入汇编

```c
#include <stdio.h>
int main(){
    int a;
    int b;
    int c;
    
    __asm
    {
        mov a,3
        mov b,4
        mov eax,a
        add eax,b
        mov c,eax   
    }
    
    printf("%d\n",c);
    return 0;
}
```



## 常用函数积累

### scanf

> 1. 用于存储字符串的空间必须足够大，防止溢出
> 2. 遇到 空格 、\n 终止
> 3. 利用==正则表达式==
>
> ```c
> scanf("%[^\n]s",str);  	//接收除了 \n 之外的数据
> ```





### exit

> 1. 直接退出当前程序
> 2. 在main种可以代替return，在函数中会直接退出程序



## 数据类型

### 常量和变量

- 常量：不会变化的数据

1. "hello"、'A'、-10、3.14

2. #define PI 3.14（==没有；==）

3. const 关键字：被修饰的变量，变为==只读==（不推荐，可以被指针改地址改掉）（又称==只读变量==）

   ```c
   cosnt int a = 10;
   ```

   

- 变量：会变化的数据

1. 变量的定义

```c
int a = 40;
```

2. 声明

```c
int a; 			//没有变量值的变量定义 叫做声明
extern int a;   //利用关键字extern
```

> 变量定义会开辟内存空间，声明变量不会开辟内存空间
>
> 当编译器编译程序时，在变量使用之前，如果没看到变量定义，编译器将变量声明提升为定义
>
> 提升为定义后，不同操作系统给定的默认值不同
>
> 如果有extern关键字，无法提升至定义



- 标识符

1. 变量和常量的统称
2. 命名规则
   1. 常量用大写、变量用小写。大小写严格区分
   2. 只能使用字母、数字、下划线。数字不能开头



### 整型的打印格式

| 符号 | 作用                         |
| :--- | ---------------------------- |
| %u   | 打印无符号int类型            |
| %d   | 打印有符号的10进制数         |
| %hd  | 打印有符号short类型          |
| %ld  | 打印有符号long类型           |
| %lld | 打印有符号long long类型      |
| %hu  | 打印无符号short类型          |
| %lu  | 打印无符号long类型           |
| %llu | 打印无符号long long类型      |
| %c   | 打印字符                     |
| %f   | 打印单精度浮点数             |
| %lf  | 打印双精度浮点数             |
| %p   | 打印地址                     |
| %x   | 打印16进制数字，字母小写输出 |
| %X   | 打印16进制数字，字母大写输出 |

### sizeof

1. 不是函数
2. 返回值为==size_t== （unsigned int）



### 字符类型char

1. 存储一个字符

​     'A' 、'@'

2. 格式匹配符 %c
3. ==ASCII码==（符号和数字 对应）



### ASCII表

| ASCII值 | 控制字符 | ASCII值 | **字符** | ASCII值 | **字符** | ASCII值 | **字符** |
| :-----: | :------: | :-----: | :------: | :-----: | :------: | :-----: | :------: |
|    0    |   NUT    |   32    | (space)  |   64    |    @     |   96    |    、    |
|    1    |   SOH    |   33    |    !     |   65    |    A     |   97    |    a     |
|    2    |   STX    |   34    |    "     |   66    |    B     |   98    |    b     |
|    3    |   ETX    |   35    |    #     |   67    |    C     |   99    |    c     |
|    4    |   EOT    |   36    |    $     |   68    |    D     |   100   |    d     |
|    5    |   ENQ    |   37    |    %     |   69    |    E     |   101   |    e     |
|    6    |   ACK    |   38    |    &     |   70    |    F     |   102   |    f     |
|    7    |   BEL    |   39    |    ,     |   71    |    G     |   103   |    g     |
|    8    |    BS    |   40    |    (     |   72    |    H     |   104   |    h     |
|    9    |    HT    |   41    |    )     |   73    |    I     |   105   |    i     |
|   10    |    LF    |   42    |    *     |   74    |    J     |   106   |    j     |
|   11    |    VT    |   43    |    +     |   75    |    K     |   107   |    k     |
|   12    |    FF    |   44    |    ,     |   76    |    L     |   108   |    l     |
|   13    |    CR    |   45    |    -     |   77    |    M     |   109   |    m     |
|   14    |    SO    |   46    |    .     |   78    |    N     |   110   |    n     |
|   15    |    SI    |   47    |    /     |   79    |    O     |   111   |    o     |
|   16    |   DLE    |   48    |    0     |   80    |    P     |   112   |    p     |
|   17    |   DCI    |   49    |    1     |   81    |    Q     |   113   |    q     |
|   18    |   DC2    |   50    |    2     |   82    |    R     |   114   |    r     |
|   19    |   DC3    |   51    |    3     |   83    |    S     |   115   |    s     |
|   20    |   DC4    |   52    |    4     |   84    |    T     |   116   |    t     |
|   21    |   NAK    |   53    |    5     |   85    |    U     |   117   |    u     |
|   22    |   SYN    |   54    |    6     |   86    |    V     |   118   |    v     |
|   23    |    TB    |   55    |    7     |   87    |    W     |   119   |    w     |
|   24    |   CAN    |   56    |    8     |   88    |    X     |   120   |    x     |
|   25    |    EM    |   57    |    9     |   89    |    Y     |   121   |    y     |
|   26    |   SUB    |   58    |    :     |   90    |    Z     |   122   |    z     |
|   27    |   ESC    |   59    |    ;     |   91    |    [     |   123   |    {     |
|   28    |    FS    |   60    |    <     |   92    |    /     |   124   |    \|    |
|   29    |    GS    |   61    |    =     |   93    |    ]     |   125   |    }     |
|   30    |    RS    |   62    |    >     |   94    |    ^     |   126   |    `     |
|   31    |    US    |   63    |    ?     |   95    |    _     |   127   |   DEL    |





### 实型（浮点型）

float：单精度浮点型（保留6位小数）

double：双精度浮点型

> 小数4.456（默认double类型）
>
> 4.456f（float类型）
>
> %.3f（保留3位小数，对第四位四舍五入）
>
> %08.3f（保留3位小数，==所有符号==加起来占8个位置，不足的位置用0补齐）

> 科学计数法：3.2e3f = 3.2 * 10^3^ = 3200





### 进制转换





### 原码反码补码

计算机采用==补码==的形式存储数据

43 - 27 ==》 43 + （-27）补码形式计算

> 规定 1000 0000 表示 -128 的==原码反码补码==
>
> 圆盘先对称 再少一个-0 最后倒过来



### 类型限定符

| **限定符** | **含义**                                                     |
| ---------- | ------------------------------------------------------------ |
| extern     | 声明一个变量，extern声明的变量没有建立存储空间。             |
| const      | 定义一个常量，常量的值不能修改。                             |
| Volatile   | 防止编译器优化代码  ;例如，小灯灭亮灭亮灭 被优化为 一个灭的状态 |
| register   | 定义寄存器变量，提高效率。register是建议型的指令，而不是命令型的指令，如果CPU有空闲寄存器，那么register就生效，如果没有空闲寄存器，那么register无效。 |



### 字符串

双引号内的一串字符

结束标记 ==\0==

打印字符串%s，找到==\0==才停止



### putchar函数

输出一个字符到屏幕

直接使用ASCII码

常用来打印换行

```c
putchar('abc');
//结果时b把a覆盖，c把b覆，最后为c
```



### scanf

1. VS2019怕用户输入的数据超出范围，导致丢失，报错

![image-20230127132542253](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230127132542253.png)

> 宏定义==最好放在第一行==

> ```c
> #pragma warning(disable:4996)  		//让编译器不要报错
> ```

2. 碰到 空格 和 换行 会自动终止

> 不能用scanf接收 ==带有空格的字符串==（用正则表达式可以）



### getchar函数

获取用户输入的一个字符

直接使用ASCII码



## 运算符和表达式

### 运算符分类

| **运算符类型** | **作用**                               |
| :------------: | :------------------------------------- |
|   算术运算符   | 用于处理四则运算                       |
|   赋值运算符   | 用于将表达式的值赋给变量               |
|   比较运算符   | 用于表达式的比较，并返回一个真值或假值 |
|   逻辑运算符   | 用于根据表达式的值返回真值或假值       |
|    位运算符    | 用于处理数据的位运算                   |
|  sizeof运算符  | 用于求字节数长度                       |



### 算术运算符

| **运算符** |  **术语**  |  **示例**   | **结果**  |
| :--------: | :--------: | :---------: | :-------: |
|     +      |    正号    |     +3      |     3     |
|     -      |    负号    |     -3      |    -3     |
|     +      |     加     |   10 + 5    |    15     |
|     -      |     减     |   10 - 5    |     5     |
|     *      |     乘     |   10 * 5    |    50     |
|     /      |     除     |   10 / 5    |     2     |
|     %      | 取模(取余) |   10 % 3    |     1     |
|     ++     |  前缀自增  | a=2; b=++a; | a=3; b=3; |
|     ++     |  后缀自增  | a=2; b=a++; | a=3; b=2; |
|     --     |  前缀自减  | a=2; b=--a; | a=1; b=1; |
|     --     |  后缀自减  | a=2; b=a--; | a=1; b=2; |



### 赋值运算符

| **运算符** | **术语** |  **示例**  | **结果**  |
| :--------: | :------: | :--------: | :-------: |
|     =      |   赋值   | a=2; b=3;  | a=2; b=3; |
|     +=     |  加等于  | a=0; a+=2; |   a=2;    |
|     -=     |  减等于  | a=5; a-=3; |   a=2;    |
|     *=     |  乘等于  | a=2; a*=2; |   a=4;    |
|     /=     |  除等于  | a=4; a/=2; |   a=2;    |
|     %=     |  模等于  | a=3; a%2;  |   a=1;    |



### 比较运算符

C语言中，真用'1',  假用'0'

| **运算符** | **术语** | **示例** | **结果** |
| :--------: | :------: | :------: | :------: |
|     ==     |  相等于  |  4 == 3  |    0     |
|     !=     |  不等于  |  4 != 3  |    1     |
|     <      |   小于   |  4 < 3   |    0     |
|     >      |   大于   |  4 > 3   |    1     |
|     <=     | 小于等于 |  4 <= 3  |    0     |
|     >=     | 大于等于 |  4 >= 1  |    1     |



### 逻辑运算符

| **运算符** | **术语** | **示例** |                         **结果**                         |
| :--------: | :------: | :------: | :------------------------------------------------------: |
|     !      |    非    |    !a    |       如果a为假，则!a为真；  如果a为真，则!a为假。       |
|     &&     |    与    |  a && b  |          如果a和b都为真，则结果为真，否则为假。          |
|    \|\|    |    或    | a \|\| b | 如果a和b有一个为真，则结果为真，二者都为假时，结果为假。 |

> C语言中，&&是 短路与,||是短路或。（java是逻辑或，逻辑与）
>
> ```c
> int i = 0, a = 0, b = 2, c = 3;
> i = a++ && ++b && c++;
> printf("a =%d\n b =%d\n c =%d\n d =%d\n", a, b, c); //1 2 3
> ```
>
> &&结合方向，从左到右，左边为假，右边不用判断，所以b、c不变

> ```c
> a = 0, b = 2, c = 3;
> i = a++||++b||c++;
> printf(" a = %d\n b = %d\n d = %d\n", a, b, d);//1 3 3
> ```
>
> ||结合方向，从左到右，左边为真，右边不用判断，所以c=3



### 运算符优先级

| **优先级** | **运算符** |  **名称或含义**  |        **使用形式**        | **结合方向** |  **说明**  |
| :--------: | :--------: | :--------------: | :------------------------: | :----------: | :--------: |
|   **1**    |    [ ]     |     数组下标     |     数组名[常量表达式]     |    左到右    |            |
|            |    ( )     |      圆括号      |  (表达式）/函数名(形参表)  |      --      |            |
|            |     .      | 成员选择（对象） |        对象.成员名         |      --      |            |
|            |     ->     | 成员选择（指针） |      对象指针->成员名      |      --      |            |
|   **2**    |     -      |    负号运算符    |          -表达式           |    右到左    | 单目运算符 |
|            |     ~      |  按位取反运算符  |          ~表达式           |              |            |
|            |     ++     |    自增运算符    |     ++变量名/变量名++      |              |            |
|            |     --     |    自减运算符    |     --变量名/变量名--      |              |            |
|            |     *      |    取值运算符    |         *指针变量          |              |            |
|            |     &      |   取地址运算符   |          &变量名           |              |            |
|            |     !      |   逻辑非运算符   |          !表达式           |              |            |
|            |   (类型)   |   强制类型转换   |      (数据类型)表达式      |      --      |            |
|            |   sizeof   |    长度运算符    |       sizeof(表达式)       |      --      |            |
|   **3**    |     /      |        除        |       表达式/表达式        |    左到右    | 双目运算符 |
|            |     *      |        乘        |       表达式*表达式        |              |            |
|            |     %      |   余数（取模）   |   整型表达式%整型表达式    |              |            |
|   **4**    |     +      |        加        |       表达式+表达式        |    左到右    | 双目运算符 |
|            |     -      |        减        |       表达式-表达式        |              |            |
|   **5**    |     <<     |       左移       |        变量<<表达式        |    左到右    | 双目运算符 |
|            |     >>     |       右移       |        变量>>表达式        |              |            |
|   **6**    |     >      |       大于       |       表达式>表达式        |    左到右    | 双目运算符 |
|            |     >=     |     大于等于     |       表达式>=表达式       |              |            |
|            |     <      |       小于       |       表达式<表达式        |              |            |
|            |     <=     |     小于等于     |       表达式<=表达式       |              |            |
|   **7**    |     ==     |       等于       |       表达式==表达式       |    左到右    | 双目运算符 |
|            |     !=     |      不等于      |      表达式!= 表达式       |              |            |
|   **8**    |     &      |      按位与      |       表达式&表达式        |    左到右    | 双目运算符 |
|   **9**    |     ^      |     按位异或     |       表达式^表达式        |    左到右    | 双目运算符 |
|   **10**   |     \|     |      按位或      |       表达式\|表达式       |    左到右    | 双目运算符 |
|   **11**   |     &&     |      逻辑与      |       表达式&&表达式       |    左到右    | 双目运算符 |
|   **12**   |    \|\|    |      逻辑或      |      表达式\|\|表达式      |    左到右    | 双目运算符 |
|   **13**   |     ?:     |    条件运算符    | 表达式1?  表达式2: 表达式3 |    右到左    | 三目运算符 |
|   **14**   |     =      |    赋值运算符    |        变量=表达式         |    右到左    |     --     |
|            |     /=     |     除后赋值     |        变量/=表达式        |      --      |            |
|            |     *=     |     乘后赋值     |        变量*=表达式        |      --      |            |
|            |     %=     |    取模后赋值    |        变量%=表达式        |      --      |            |
|            |     +=     |     加后赋值     |        变量+=表达式        |      --      |            |
|            |     -=     |     减后赋值     |        变量-=表达式        |      --      |            |
|            |    <<=     |    左移后赋值    |       变量<<=表达式        |      --      |            |
|            |    >>=     |    右移后赋值    |       变量>>=表达式        |      --      |            |
|            |     &=     |   按位与后赋值   |        变量&=表达式        |      --      |            |
|            |     ^=     |  按位异或后赋值  |        变量^=表达式        |      --      |            |
|            |    \|=     |   按位或后赋值   |       变量\|=表达式        |      --      |            |
|   **15**   |     ，     |    逗号运算符    |       表达式,表达式        |    左到右    |            |



### 类型转换

- 隐式类型转换

1. 编译器自动完成
2. 由赋值产生的类型转换



> 类型转换的原则:
>
> 占用内存字节数少(值域小)的类型，向占用内存字节数多(值域大)的类型转换，以保证精度不降低。

![2016-06-02_202741](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/clip_image002.jpg)



```c
int r = 3;
float s = 3.14 * r * r; //左值float类型， 右值double类型
						//会不会丢失数据，取决于数据范围
```



- 强制类型转换

大多数用于形参给实参传值



## 程序流程结构

### 选择结构

#### if分支

```C
#include <stdio.h>
int main(){
    int a = 5;
    if( a > 5 )
    {
        printf("a>5\n");
    }
    else if( a < 2 )
    {
        printf("a<2\n");
    }
    else
    {
        printf("not find");
    }
    return 0;
}
```



#### switch分支

```c
#include <stdio.h>
int main(){
    int score;
    scanf("%d",&score);
    
    switch(score / 10)
    {
        case 10:
            printf("excellent");
            break; 
        case 9:
            printf("excellent");
            break;
        case 8:
            printf("good");
            break;
        default:
            printf("bad");
            break;        
    }
    return 0;
}
```

> case穿透：
>
> 没有break，会向下穿透继续执行



### 循环结构

#### while循环

```c
#include <stdio.h>
int main(){
    int score;
    scanf("%d",&score);
    while(score < 60)
    {
        printf("低于60不给毕业\n");
    	scanf("%d",&score);
    }
    return 0;
}
```



#### do while循环

```c
#include <stdio.h>
int main(){
    int a = 0;
    do
    {
        a++;

    }while(a > 10);
    return 0;
}
```



#### for循环

```C
#include <stdio.h>
int main(){
    //求1-100的和
    int i = 0;		//循环因子
    int sum = 0;
	for(i = 1; i <= 100; i++)
    {
        sum = sum + i;
    }
    return 0;
}
```

> 1. 循环因子可以定义在for结构内
> 2. for的3个表达式可以省略，但2个分号（；）不能省略



### 跳转语句

#### break

> 1. 跳出一重循环
> 2. 防止case穿透



#### continue

> 1. 结束本次循环



#### goto

```C
#include <stdio.h>
int main(){
	printf("1");
    printf("2");
TOP:
    printf("3");
    printf("4");
    printf("5");
    goto TOP;
    return 0;
}
```

> 1. 设置标签
> 2. 利用 goto关键字



## 数组和字符串

### 一维数组

4种定义数组的方法

```c
//定义一个数组，同时初始化所有成员变量
int a[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

//初始化前三个成员，后面所有元素都设置为0
int a[10] = { 1, 2, 3 };

//所有的成员都设置为0
int a[10] = { 0 };
	
//[]中不定义元素个数，定义时必须初始化
int a[] = { 1, 2, 3, 4, 5 };

```



### 二维数组

- 初始化

```C
//常规初始化
int arr[3][5] = { {1, 2, 3, 4, 5},{2, 4, 6, 8, 10},{1,1,1,1,1}};

//不完全初始化,默认为0
int arr[3][5] = { {1, 2},{2, 4, 8, 10},{1,1,1,1,1}};

//初始化全0的二维数组
int arr[3][5] = {0}；
    
//系统自动分配行列
int arr[3][5] = {1,2,3,4,5,6,7,8,9,10,21};

//只能省略行值，不能省略列值
int arr[][3] = {1,2,3,4,5};
```



### 多维数组

```c
//2层2行2列
int arr[2][2][2] = {{1，2，3，4}，{5，6，7，8}}，
    			   {{1，2，3，4}，{5，6，7，8}} ;		
```



### 柔性数组

> 柔性数组（flexible array）
>
> C99 中，结构体中的==最后一个元素==允许是未知大小的数组，这就叫做『柔性数组』成员
>
> 柔性数组的大小是可以调整的

#### 柔性数组的特点

> 1. 结构体中的柔性数组成员前面必须至少一个其他成员。 
> 2. sizeof 返回的这种结构体大小不包括柔性数组的内存。 
> 3. 包含柔性数组成员的结构体用malloc ()函数进行内存的动态分配，并且分配的内存应该大于结构的大小，以适应柔性数组的预期大小。

#### 为什么要有柔性数组

> 1. 减少内存开辟的次数，减少忘记释放内存的可能性
> 2. 用malloc开辟空间，次数越多，==太多内存碎片==，空间利用率差
> 3. 开辟的内存空间，是==连续的空间==，访问效率更高



> ```C
> struct S{
>     int n;
>     int arr[0];
> };
> 
> //如果编译不通过，则
> struct S{
>     int n;
>     int arr[];
> };
> printf("%d\n",sizeof(struct S));  //  4
> ```

> 如何使用？
>
> ```C
> struct S{
>     int n;
>     int arr[0];
> };
> int main(){
>     struct S* ps = (struct S*)malloc(sizeof(struct S) + 5*sizeof(int));
>     ps->n = 100;
>     int i = 0;
>     for(i = 0; i < 5; i++){
>         ps->arr[i] = i;
>     }
>     struct S* ptr = realloc(ps,44); // 一共开辟1个int + 10个int
>     if(ptr != NULL){
>         ps = ptr; //开辟成功 则赋值
>     }
>     for(i = 5; i < 10; i++){
>         ps->arr[i] = i;
>     }
>     
>     for(i = 0; i < 10; i++){
>         printf("%d\n",ps->arr[i];
>     }
>     //释放内存
>     free(ps);
>     ps = NULL;
> }
> ```
>
> 同样作用，可以写成
>
> ```C
> struct S{
>     int n;
>     int* arr;
> };
> int main(){
>     struct S* ps = (struct S*)malloc(sizeof(struct S));
>     ps->arr = (int*)malloc(5*sizeof(int));
> 
>     int i = 0;
>     for(i = 0; i < 5; i++){
>         ps->arr[i] = i;
>     }
>     
>     int * ptr = realloc(ps->arr,10*sizeof(int)); //调整大小
>     if(ptr != NULL){
>         ps = ptr; //开辟成功 则赋值
>     }
>     for(i = 5; i < 10; i++){
>         ps->arr[i] = i;
>     }
>     
>     for(i = 0; i < 10; i++){
>         printf("%d\n",ps->arr[i];
>     }
>     //释放内存
>     free(ps->arr);
>     ps->arr = NULL;
>     free(ps);
>     ps = NULL;
> }
> ```



### 字符数组、字符串

- 异同

```c
char str[6] = {'h', 'e', 'l', 'l', 'o'，'\0'};
//等同于
char str[] = "hello"; //自动补 \0
```



- 处理字符串的函数

1. gets()

> char * gets(char * s);
>
> 从键盘获取一个字符串，返回字符串的首地址。==可以获取带有空格==的字符串。
>
> 参数：用来存储字符串的空间地址
>
> 返回值：返回实际获取到的字符串首地址

```c
char str[100];
printf("%s\n",gets(str));
//获取一个字符串，返回字符串的首地址
//字符串可以带空格
//如果str空间太小，存储的数据会部分丢失
```



2. fgets()

> char * fgets(char * s, int size, FILE * stream);
>
> 从stdin获取一个字符串，==预留\0==的存储空间。
>
> 参数1：用来存储字符串的空间地址
>
> 参数2：描述空间的大小
>
> 参数3：读取字符串的位置
>
> 返回值：返回实际获取到的字符串首地址

```c
char str[100];
printf("%s\n",fgets(str, sizeof(str), stdin));
//预留 \0 的存储空间
//空间足够会读 \n ， 不足则舍弃
 
```



3. puts()

> int puts( const char * s);
>
> 将一个字符串输出到屏幕，==自动添加换行符==（专门写出到屏幕，所以需要换行）
>
> 参数：待写出到屏幕的字符串
>
> 返回值：失败返回 -1 ， 成功返回 非负数



4. fputs()

> int fputs(const char * str, FILE * stream);
>
> 将一个字符串输出到屏幕，==不会自动添加换行符==
>
> 参数1：待写出到屏幕的字符串
>
> 参数2：写出位置 stdout
>
> 返回值：失败返回 -1 ， 成功返回 非负数



5. strlen()

> size_t strlen(const char * s);
>
> 获取字符串的有效长度，==不包含\0== ，到\0就必须结束 strlen（"hello\0world"）==>  5
>
> 参数1：待求长度的字符串
>
> 返回值：有效的字符个数



## 函数

### 函数的分类

- 系统函数，即库函数

- 用户定义函数

### 函数的作用

> 1. 提高代码的复用性
> 2. 提高程序模块化

### 函数的定义

>  函数原型包含
>
> 1. 返回值类型
> 2. 函数名
> 3. 形参列表

> 函数体包含
>
> 1. 一对大括号
> 2. 代码块

> 函数调用包括
>
> 1. 函数名
> 2. 实参列表

### 函数声明

> 函数调用之前，编译没有见过函数定义，就需要函数声明

> 编译器自动隐式声明：返回值为int，补全函数名和形参列表（==不要依赖==）

### 多文件联编

> 将多个含有不同函数功能的 .c 文件模块，编译到一起，生产一个 .exe 文件

> 防止头文件重复包含
>
> 1. #pragma once （只导入一次）-----在windows种
> 2. #ifndef \_\_HEAD_H__
>
> ​      #define  \_\_HEAD_H__
>
> ​		头文件内容......（函数声明、include头文件、类型定义、宏定义）
>
> ​		#endif



### 字符函数

### strlen

> size_t strlen ( const char * str );
>
> 参数1：指向的字符串必须要以 '\0' 结束
>
> 返回值：size_t，是无符号的



> 模拟实现
>
> 方式1：
>
> ```C
> //计数器方式
> int my_strlen(const char * str)
> {
>  	int count = 0;
>  	while(*str)
> 	{
>  		count++;
>  		str++;
>  	}
>      return count;
> }
> ```
>
>  方式2：
>
> ```C
> //不能创建临时变量计数器
> int my_strlen(const char * str)
> {
>      if(*str == '\0')
>      	return 0;
>      else
>      	return 1 + my_strlen(str+1);
> }
> ```
>
> 方式3：
>
> ```c
> //指针 - 指针 的方式
> int my_strlen(char *s)
> {
>        char *p = s;
>        while(*p != ‘\0’ )
>               p++;
>        return p-s;
> }
> 
> ```



### strcpy

> char* strcpy(char * destination, const char * source );
>
> - 源字符串必须以 '\0' 结束。 
> - 会将源字符串中的 '\0' 拷贝到目标空间。 
> - 目标空间必须足够大，以确保能存放源字符串。 
> - 目标空间必须可变。

> 模拟实现
>
> ```C
> //1.参数顺序
> //2.函数的功能，停止条件
> //3.assert
> //4.const修饰指针
> //5.函数返回值
> //6.题目出自《高质量C/C++编程》书籍最后的试题部分
> char *my_strcpy(char *dest, const char*src)
> { 
> 	 char *ret = dest;
> 	 assert(dest != NULL);
>  	 assert(src != NULL);
>  
>      while((*dest++ = *src++)) //src的字符放到dest，当src为\0时，dest赋为0，并退出while
>      {
>            ;
>      }
>      return ret;
> }
> ```



### strcat

> char * strcat ( char * destination, const char * source );
>
> - 源字符串必须以 '\0' 结束。 
> - 目标空间必须有足够的大，能容纳下源字符串的内容。
> -  目标空间必须可修改。



> 模拟实现
>
> ```c
> char *my_strcat(char *dest, const char*src)
> {
> 	 char *ret = dest;
> 	 assert(dest != NULL);
>  	 assert(src != NULL);
> 	 while(*dest)
> 	 {
>  		dest++;
> 	 }
> 	 while((*dest++ = *src++)) //简洁的代码，src后的\0也赋值给了dest
>  	 {
> 	      ;
> 	 }
> 	 return ret;
> }
> 
> ```



### strcmp

> int strcmp ( const char * str1, const char * str2 );
>
> - 第一个字符串大于第二个字符串，则返回大于0的数字 
> - 第一个字符串等于第二个字符串，则返回0 
> - 第一个字符串小于第二个字符串，则返回小于0的数字

> 模拟实现
>
> ```c
> int my_strcmp (const char * src, const char * dest)
> {
>         assert(src != NULL);
>         assert(dest != NULL);
>         while( *src == *dest)
>         {
>             if(*dst == '\0')
>                 return 0;
>             ++src;
>             ++dest;
>         }
> 
>         if (*src > *dest)
>             return 1;
>         else
>         	return -1 ;
> }
> ```
>
> 

### strncpy

> char * strncpy ( char * destination, const char * source, size_t num );
>
> - 拷贝num个字符从源字符串到目标空间。 
> - 如果源字符串的长度小于num，则拷贝完源字符串之后，在目标的后边追加0，直到num个。



### strncat

> char * strncat ( char * destination, const char * source, size_t num );
>
> - sou按num个字符拼接到des



### strstr

> char * strstr ( const char *str1, const char * str2);
>
> - 查找字符串 ：在str1中 找 第一次出现 str2 字符串的 地址
> - KMP算法

> 模拟实现
>
> ```c
> char * my_strstr (const char * str1, const char * str2)
> {   
>     assert(str1 != NULL);
>     assert(str2 != NULL);
>     char *s1;
>     char *s2;
>     char *cur = str1;
>     if ( *s2 == '\0')     
>         return s1;
>     while (*cur)
>     {
>         s1 = cur;
>         s2 = str2;
>         while ( (*s1 != '\0') && (*s2 != '\0') && (*s1 == *s2) ) {
>             s1++;
>             s2++;
>         }
>         if(*s2 == '\0')
>             return cur;
>   		cur++;
>     }
>     return NULL;
> }
> ```
>
> 

### strtok

> char * strtok ( char * str, const char * sep );
>
> - sep参数是个字符串，定义了用作分隔符的字符集合 
> - 第一个参数指定一个字符串，它包含了0个或者多个由sep字符串中一个或者多个分隔符分割的标记。
> - strtok函数找到str中的下一个标记，并将其用 \0 结尾，返回一个指向这个标记的指针。（注： strtok函数会改变被操作的字符串，所以在使用strtok函数切分的字符串一般都是==临时拷贝的内容==并且可修改。） 
> - strtok函数的第一个参数不为 NULL ，函数将找到str中第一个标记，strtok函数将保存它在字符串 中的位置。
> - strtok函数的第一个参数为 NULL ，函数将在==同一个字符串中==被保存的位置开始，查找下一个标 记。 如果字符串中不存在更多的标记，则返回 NULL 指针。
> - 如果字符串中不存在更多的标记，则返回 NULL 指针。



### strerror

> char * strerror ( int errnum );
>
> - 返回错误码，所对应的错误信息。
> - strerror(errno)   errno是全局的错误码 头文件errno.h

> ```C
> perror("错误码");//错误码："错误提示"
> ```
>
> 使用==比strerror方便==

## 内存函数

### memcpy

> void * memcpy ( void * destination, const void * source, size_t num );
>
> - num是字节数
> - 函数memcpy从source的位置开始向后复制num个字节的数据到destination的内存位置。
> -  这个函数在遇到 '\0' 的时候并不会停下来。
> -  如果source和destination有任何的重叠，复制的结果都是未定义的。
> - ==不能有重叠==

> 模拟实现
>
> ```c
> void * my_memcpy(void* dest , const void * src , size_t num)
> {
>     void* ret = dest;
>     assert(dest != NULL);
>     assert(src != NULL);
>     while(num--){
>         *(char*)dest = *(char*)src;
>         ++(char*)dest;
>         ++(char*)src;
>     }
>     return ret;
> }
> ```
>



### memmove

> void * memmove ( void * destination, const void * source, size_t num );
>
> - 和memcpy的差别就是memmove函数处理的源内存块和目标内存块是==可以重叠==的。 
> - 如果源空间和目标空间出现重叠，就得使用memmove函数处理。

> 模拟实现
>
> ```c
> void * my_memmove(void * dest, void * src , size_t num){
>     assert(dest != NULL);
>     assert(src != NULL);
>     void* ret = dest;
>     if(dest < src || dest > (char*)src + count) //src从前向后拷贝 dest在前 src在后 
>     {
>         while(count--){
>         	*(char*)dest = *(char*)src;
>         	++(char*)dest;
>         	++(char*)src;        
>         }
>     }
>     else
>     {
>         //src从后往前拷贝 dest在后 src在前
>         while(count--)
>         {
>         	*( (char*)dest + count) = *( (char*)src + count);
>         }
>     }
>     return ret;
> }
> ```



### memcmp

> int memcmp(const void* buf1, const void* buf2, size_t num);
>
> - 比stcmp高级，可以比较内存



### memset

>  void* memset(void* dest,int c, size_t count);
>
> 参数1：目的地
>
> 参数2：放什么内容
>
> 参数3：设置几个字节
>
> - 内存设置



### 字符分类函数

|   函数   | 符合条件返回 真                                              |
| :------: | :----------------------------------------------------------- |
| iscntrl  | 任何控制字符                                                 |
| isspace  | 空白字符：空格‘ ’，换页‘\f’，换行'\n'，回车‘\r’，制表符'\t'或者垂直制表符'\v' |
| isdigit  | 十进制数字 0~9                                               |
| isxdigit | 十六进制数字，包括所有十进制数字，小写字母a~f，大写字母A~F   |
| islower  | 小写字母a~z                                                  |
| isupper  | 大写字母A~Z                                                  |
| isalpha  | 字母a~z 或 A~Z                                               |
| isalnum  | 字母或者数字，a~z,A~Z,0~9                                    |
| ispunct  | 标点符号，任何不属于数字或者字母的图形字符（可打印）         |
| isgraph  | 任何图形字符                                                 |
| isprint  | 任何可打印字符，包括图形字符和空白字符                       |



### 字符转换函数

|  函数   | 功能       |
| :-----: | :--------- |
| tolower | 转换成小写 |
| toupper | 转换成大写 |

## 指针

### 看不懂这些再去对应学习

> 基础指针
>
> ```c
> //指针数组
> int* arr[10];
> //数组指针
> int* (*arr)[10] = &arr;
> //函数指针
> int(*pAdd)(int, int);
> //函数指针的数组
> int(*pArr[5])(int, int);
> //指向函数指针数组的指针
> int(*（*ppArr)[5])(int, int) = &pArr;
> ```
>



> 笔试题
>
> 知识点：
>
> 1. 除了 ==sizeof（数组名）== 和 ==&数组名== 其他 ==数组名==都为首元素地址
> 2. 32位/64位平台地址为 ==4字节/8字节==
> 3. arr[0]   <= = 等价于 = =>  *(arr+0)
>
> 
>
> ```c
> //一维数组（视频对应指针详解8）
> int a[] = {1,2,3,4};
> printf("%d\n",sizeof(a));		//16       sizeof（数组名） 代表整个数组
> printf("%d\n",sizeof(a+0));		//4、8		   指针的大小是 4、8
> printf("%d\n",sizeof(*a));		//4		   首元素int类型
> printf("%d\n",sizeof(a+1));		//4、8	  指针的大小是 4、8
> printf("%d\n",sizeof(a[1]));	//4		   某个元素的类型是int		
> printf("%d\n",sizeof(&a));		//4、8	  指针（地址）的大小是 4、8
> printf("%d\n",sizeof(*&a));		//16	   整个数组的大小是 16
> printf("%d\n",sizeof(&a+1));	//4、8	  指针的大小是 4、8
> printf("%d\n",sizeof(&a[0]));	//4、8	  指针的大小是 4、8
> printf("%d\n",sizeof(&a[0]+1));	//4、8	  指针的大小是 4、8	
> ```
>
> 
>
> ```c
> //字符数组
> char arr[] = {'a','b','c','d','e','f'};
> printf("%d\n", sizeof(arr));		//6  	  错题！！！ 别把\0带上 sizeof有啥算啥
> printf("%d\n", sizeof(arr+0));		//4、8
> printf("%d\n", sizeof(*arr));		//1
> printf("%d\n", sizeof(arr[1]));		//1
> printf("%d\n", sizeof(&arr));		//4、8	 错题！！！
> printf("%d\n", sizeof(&arr+1));		//4、8
> printf("%d\n", sizeof(&arr[0]+1));	//4、8
> 
> printf("%d\n", strlen(arr));		//随机值	错题！！！
> printf("%d\n", strlen(arr+0));		//随机值
> printf("%d\n", strlen(*arr));		//err     错题！！！ 相当于把97传入strlen
> printf("%d\n", strlen(arr[1]));		//err
> printf("%d\n", strlen(&arr));		//随机值
> printf("%d\n", strlen(&arr+1));		//随机值 - 6
> printf("%d\n", strlen(&arr[0]+1));	//随机值 - 1
> 
> char arr[] = "abcdef";
> printf("%d\n", sizeof(arr));		//7
> printf("%d\n", sizeof(arr+0));		//4、8
> printf("%d\n", sizeof(*arr));		//1
> printf("%d\n", sizeof(arr[1]));		//1
> printf("%d\n", sizeof(&arr));		//4、8
> printf("%d\n", sizeof(&arr+1));		//4、8
> printf("%d\n", sizeof(&arr[0]+1));	//4、8
> 
> printf("%d\n", strlen(arr));		//6
> printf("%d\n", strlen(arr+0));		//6
> printf("%d\n", strlen(*arr));		//err
> printf("%d\n", strlen(arr[1]));		//err
> printf("%d\n", strlen(&arr));		//6       会有警告 strlen需要的是const char*类型 
> printf("%d\n", strlen(&arr+1));		//随机值	但是给的是 char（*）[7]类型
> printf("%d\n", strlen(&arr[0]+1));	//5
> 
> char *p = "abcdef";
> printf("%d\n", sizeof(p));			//4、8 	p指代的是a的地址
> printf("%d\n", sizeof(p+1));		//4、8
> printf("%d\n", sizeof(*p));			//1
> printf("%d\n", sizeof(p[0]));		//1		重点！！！ arr[0] == *(arr+0) 指针当作数组
> printf("%d\n", sizeof(&p));			//4、8	地址的地址还是地址
> printf("%d\n", sizeof(&p+1));		//4、8
> printf("%d\n", sizeof(&p[0]+1));	//4、8
> 
> printf("%d\n", strlen(p));			//6
> printf("%d\n", strlen(p+1));		//5
> printf("%d\n", strlen(*p));			//err  相当于把97传入strlen 非法访问
> printf("%d\n", strlen(p[0]));		//err	
> printf("%d\n", strlen(&p));			//随机值  错题！！！ a地址的地址里面何时碰到\0未知	
> printf("%d\n", strlen(&p+1));		//随机值  错题！！！
> printf("%d\n", strlen(&p[0]+1));	//5
> 
> ```
>



>```c
>//二维数组
>int a[3][4] = {0};
>printf("%d\n",sizeof(a));			//48		
>printf("%d\n",sizeof(a[0][0]));		//4
>printf("%d\n",sizeof(a[0]));		//16	错题！！！  a[0]是第一行的数组名
>printf("%d\n",sizeof(a[0]+1));		//4、8  错题！！！  不是第二行的地址
>									//数组名+1 ，一维数组名加减的是 里面元素
>									//	验证： *(a[0]+1) == a[0][1]
>printf("%d\n",sizeof(*(a[0]+1)));	//4     错题！！！  不是第二行的数组名解引用
>printf("%d\n",sizeof(a+1));			//4、8	数组名是首元素地址 第二行的地址
>									// 高维向下看低维，二维数组名加减的是 一维数组名
>									//  验证： *(a+1) == a[1]
>printf("%d\n",sizeof(*(a+1)));		//16
>printf("%d\n",sizeof(&a[0]+1));		//4、8	第二行数组a[1]的地址
>printf("%d\n",sizeof(*(&a[0]+1)));	//16
>printf("%d\n",sizeof(*a));			//16	数组名是首元素地址
>printf("%d\n",sizeof(a[3]));		//16	错题！！！  sizeof不参与运算 相当于a[0]	
>```



### 笔试题

> ```c
> int main()
> {
>     int a[5] = { 1, 2, 3, 4, 5 };
>     int *ptr = (int *)(&a + 1);
>     printf( "%d,%d", *(a + 1), *(ptr - 1));
>     return 0;
> }
> //程序的结果是什么？
> 
> //   2，5
> ```
>
>  
>
> ```c
> //已知，结构体Test类型的变量大小是20个字节
> struct Test
> {
>  int Num;
>  char *pcName;
>  short sDate;
>  char cha[2];
>  short sBa[4];
> }*p;
> //假设p 的值为0x100000。 如下表表达式的值分别为多少？
> 
> int main()
> {											//指针±整数 取决于指针类型
>     p = (struct Test*)0x100000；
>  printf("%p\n", p + 0x1);					//100000 + 20 ==> 0x100014
>  printf("%p\n", (unsigned long)p + 0x1);	//0x100001
>  printf("%p\n", (unsigned int*)p + 0x1);	//0x100004
>  return 0;
> }
> 
> ```
>
> ​	 



> ```C
> int main()
> {
>     int a[4] = { 1, 2, 3, 4 };
>     int *ptr1 = (int *)(&a + 1);
>     int *ptr2 = (int *)((int)a + 1);
>     printf( "%x,%x", ptr1[-1], *ptr2);
>     return 0;
> }
> //*(ptr1 - 1)
> //4，0x 02 00 00 00
> ```
>
> ![image-20230223111853740](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230223111853740-1677122335301-1-1677122338147-3-1677122350878-5.png)



> ```c
> #include <stdio.h>
> int main()
> {				//逗号表达式
>     int a[3][2] = { (0, 1), (2, 3), (4, 5) };  //1  3  5  0  0  0
>     int *p;
>     p = a[0];
>     printf( "%d", p[0]);  // 1
>  return 0;
> }
> 
> ```



> ```c
> int main()
> {
>     int a[5][5];
>     int(*p)[4]; 
>     p = a;
>     printf( "%p,%d\n", &p[4][2] - &a[4][2], &p[4][2] - &a[4][2]);
>     return 0;
> }
> // 指针 - 指针  ==》 指针之间元素的个数（有正负）
> // -4 用 %p 打印 ==》 -4的补码直接当作地址 0xFFFC
> //0xFFFC ， -4
> ```



> ```C
> int main()
> {
>     int aa[2][5] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
>     int *ptr1 = (int *)(&aa + 1);
>     int *ptr2 = (int *)(*(aa + 1));               //aa[1]
>     printf( "%d,%d", *(ptr1 - 1), *(ptr2 - 1));
>     return 0;
> }
> //10，5
> ```



> ```c
> #include <stdio.h>
> int main()
> {
>  char *a[] = {"work","at","alibaba"};
>  char**pa = a;
>  pa++;			//pa+1 ， char * * pa 的指针pa 跳过了一个char*
>  printf("%s\n", *pa);		//at
>  return 0;
> }
> ```



> ```C
> int main()
> {
>  char *c[] = {"ENTER","NEW","POINT","FIRST"};
>  char**cp[] = {c+3,c+2,c+1,c};
>  char***cpp = cp;
>  printf("%s\n", **++cpp);		//POINT
>  printf("%s\n", *--*++cpp+3);	//ER
>  printf("%s\n", *cpp[-2]+3);	//ST
>  printf("%s\n", cpp[-1][-1]+1);	//EW
>  return 0;
> }
> ```
>
> 

### 指针的定义、使用

```c
int a = 10;
int* p = &a;
*p = 250; 	// *p ： 指针的 解引用 ，间接引用
```



### 如何理解指针

- 左值、右值

```c
int m = 10;		//m在左值，n作为存储空间
int n = 20;		
n = m;			//m在右值，m作为存储空间的内容
```

同理

```C
int a = 10;
int* p = &a;		//*p : 将p的内容取出，当成地址看待，找到该地址对应的内存空间
*p = 250;			//如果为左值，作为一个存储空间
					//如果为右值，取出空间中的内容
```

> 逻辑梳理
>
> 1. 变量a作为左值，是一个存储空间的别称，空间里面放着int类型的数据，将数据10放入a
>
> 2. 变量p是一个存储int*类型的存储空间，存放着空间a的地址
>
> 3. 空间p里面放着空间a的地址，找到空间a的地址，放入数据250



### 指针、数组

> 区别
>
> 1. 指针是变量，数组名是常量
> 2. sizeof(指针)  ==》 4/8
> 3. sizeof(数组名)  ==》数组实际字节数

> 数组名：是==地址常量==，不可以被修改
>
> ```c
> int a[] = {1,2,3};
> int b[3];
> // b = a
> ```
>
> ==arr[i] == *(arr+i) == p[0] == *(p+i)==



> 全面理解指针、数组
>
> \*arr[5]： 会先结合arr[5] ，再结合\*。tips：==如果先结合*就是指针，否则就是数组==
>
> ```c
> //arr是一个有5个元素的整型数组
> int arr[5];
> //parr1是一个数组，数组有10个元素，每个元素类型是int*,parr1是指针数组
> int* parr1[10];
> //parr2是一个指针，指向了一个数组，数组有10个元素，每个元素类型是int，parr2是数组指针
> int (*parr2)[10];
> //parr3是一个数组，数组有10个元素，每个元素是一个数组指针，数组指针指向的数组有5个元素，每个元素类型是int
> int (*parr3[10])[5]
> ```
>



> 取地址  &arr 、 单独放入sizeof内部  sizeof(arr)  
>
> ==以上这两种情况==arr代表整个数组，==其他情况arr为首元素地址==
>
> ```c
> int arr[10] = { 0 };
> printf("arr = %p\n", arr);
> printf("&arr= %p\n", &arr);
> printf("arr+1 = %p\n", arr+1);
> printf("&arr+1= %p\n", &arr+1);
> ```
>
> &arr 表示的是数组的地址，而不是数组首元素的地址。
>
> &arr 的类型是： int(*)[10] ，是一种数组指针类型 数组的地址+1 跳过整个数组的大小  
>
> 所以 &arr+1 相对于 &arr 的差值是40.



> 数组指针
>
> ```c
> int arr[5];
> int(*pa)[5] = &arr; 	//pa是一个数组指针 pa的类型是int(*)[5]：指向数组的指针类型
> ```
>



### 数组传参、指针传参（重点）

> 核心概念：
>
> 1. 数组名是首元素的地址
> 2. 传进去地址，可以拿指针接收（地址就是指针）



> 一维数组传参
>
> ```c
> void test(int arr[]){}   		//没填数组元素个数也能传
> 
> void test(int arr[10]){}		//填了元素个数 肯定能传
> 
> void test(int arr[20]){}		//填错了元素个数 也能传
> 
> void test(int *arr){}			//单个数组名是首元素地址，首元素是int，所以首元素的指针是int*类型
> 
> void test2(int *arr[20]){}		//ok
> 
> void test2(int *arr[]){}		//ok
> 
> void test2(int **arr){}			//arr2是首元素的地址，首元素是int*类型，首元素的地址是int**类型
>  
> int main(){
> 	int arr[10] = {0};
> 	int *arr2[20] = {0};
> 	test(arr);					// 单个数组名是首元素的地址
> 	test2(arr2);
> }
> ```



> 二维数组传参
>
> ```C
> void test(int arr[3][5]){}			//ok
> 
> void test(int arr[][]){}			//error 
> 
> void test(int arr[][5]){}			//ok
> 
> void test(int arr[3][]){}			//error
> 
> //总结：二维数组传参，函数形参的设计只能省略第一个[]的数字。
> //因为对一个二维数组，可以不知道有多少行，但是必须知道一行多少元素。
> 
> void test(int *arr){}				//error 数组的地址不能拿整型指针接收
> 
> void test(int* arr[5]){}			//error 数组的地址不能拿指针数组接收
> 
> void test(int (*arr)[5]){}			//ok arr是一个指针，指向1个数组，数组有5个元素，每个元素是int； 传进去数组的地址，用数组指针接收
> 
> void test(int **arr){}				//error 数组的地址，不能放到二级指针里去
> int main()
> {
>   int arr[3][5] = {0};
>      test(arr);
>    }
> 
> ```



> 一级指针传参
>
> ```c
> void test1(int* p){}
> 
> void test2(char* p){}
> 
> int main(){
>     int a = 10;
>     int* p1 = &a;
>     test1(&a);		//如何传实参
>     test1(p1);
>     
>     char ch = 'w';
>     char* pc = &ch;
>     test2(&ch);
>     test2(pc);
>     
>     return 0;
> }
> ```



> 二级指针传参（3种）
>
> 1. 一级指针的地址
> 2. 二级指针变量
> 3. 存放一级指针的数组
>
> ```c
> void test1(int** ptr){}
> 
> int main(){
> int n = 10;
> int* p = &n;
> int** pp = &p;
> 
> test(pp);
> test(&p);
> 
>  //重点
> int* arr[10];
> test(arr);		//arr是首元素地址，首元素是int*类型，int*的地址是int**类型，就可以用二级指针接收了
>  return 0;
> }
> ```
>



### 函数指针

> 数组指针：指向数组的指针
>
> 函数指针：指向函数的指针

> 函数指针类型的==*必须靠近==函数名（或指针变量）(有例题说明)

> 函数指针
>
> ```c
> int Add(int x, int y){
>  int z = 0;
>  z = x + y;
>  return z;
> }
> int main(){
>  int a = 10;
>  int b = 20;
>  printf("%d",Add(a,b));
>  printf("%p",&Add);			//函数的地址
>  printf("%p",Add);			//类比数组首元素的地址，取地址函数名、函数名  都是函数的地址
> 
>  //存放函数地址的指针
>  int (*pa)(int, int) = Add;
> 
>  printf("%d", (*pa)(2,3));		//5
>  return 0;
> }
> ```



> 函数指针数组的作用：
>
> 转移表
>
> ```c
> int (*pfArr[5])(int, int) =  {0, Add, Sub, Mul, Div};
> //函数指针数组 配合 数组取出函数
> int ret = pfArr[input](x,y);
> ```



### 回调函数

> 回调函数是：通过函数指针调用的函数。
>
> 把函数的指针(地址)作为参数传递给另一个函数，当这个指针被用来调用其所指的函数时，称这是回调函数
>
> 
>
> 用转移表也能实现同样效果



> ```c
> void print(char *str){
>     printf("hehe",str)
> }
> void test(void(*p)(char*)){
>     printf("test\n");
>     p("BIT");				//通过传进来的函数指针，调用指针所指函数
> }
> int main(){
>     test(print);
>     return 0;
> }
> ```
>



### 指向函数指针的数组 的指针

> ```c
> int (*pfArr[4])(int , int); //pfArr是一个数组   ，数组里面的元素是 函数指针
> int (*(*ppfArr)[4])(int , int) = &pfArr; //ppfArr是一个数组指针，指针指向的数组有4个元素，每个元素是函数指针，所以pfArr是一个指向（函数指针数组）的指针
> ```



### 指针相关的例题

> 先掌握的基本功
>
> ```c
> int (*p)(int,int)		//p是函数指针变量
> int (*)(int,int)		//函数指针类型
> ```



> ```c
> //代码1
> (*(void (*)())0)();
>       void (*)()			//函数指针类型
>      (void (*)())0			//把0强制类型转换，相当于是个地址0
>        					//对地址解引用，调用一个无参函数
>        
> //代码2
> void (*signal(int , void(*)(int)))(int);
> 				    void(*)(int) 			//函数指针类型
>                 (int , void(*)(int))			//参数列表
>           signal(int , void(*)(int))			//函数，但是缺了返回类型
> void (*						     )(int);	//函数返回类型，恰好也是一个函数指针类型
> 											//函数指针类型的*必须靠近函数名（或指针变量）
> ```
>
> ```c
> //简化函数指针类型*必须靠近函数名（或者函数指针变量）的情况，重新定义新变量
> typedef void(*)(int) pfun_t;		//按理说这样写，但是没有*靠近
> typedef void(* pfun_t)(int);
> pfun_t signal(int,pfun_t);
> ```
>
> 

### const关键词

> const修饰变量
>
> ```c
> const int a = 20;
> int* p = &a;
> *p = 30;		//a被修改成了20
> ```
>
> const修饰指针
>
> ```C
> //4种效果的区别
> 
> //可以修改p，不能修改*p
> const int* p;
> 
> //可以修改p，不能修改*p
> int const *p;
> 
> //可以修改*p，不能修改p
> int * const p;
> 
> //不能修改p，*p
> const int * const p;
> ```
>
> 总结：const==向右==修饰，被修饰的部分即为==只读==



### 指针的大小

> 指针的大小与类型无关，只与平台架构有关。
>
> 32位：4字节
>
> 64位：8字节



### 野指针

> 1. 没有一个有效的地址空间
>
> ```c
> int* p;			//空间p里面存的是随机数
> *p = 1000;		//如果地址有效，也不一定能有权限访问
> ```
>
> 2. p变量有一个值，但该值不是可访问的内存空间
>
> ```C
> int* p = 10;		//地址0-255确定是给操作系统使用的
> *p = 1000;
> ```



### 空指针

> ```c
> int* p = NULL; 		//#define NULL ((void*)0)   NULL = 0
> *p = 300;
> ```
>
> 为了避免空指针
>
> ```c
> if(p != NULL){
>     
> }
> ```



### 万能指针、泛型指针

> 使用前，必须具体化指针的类型

```c
int a = 30;
void* p;
p = &a;
printf("%d", *((int*)p) );
```



## 结构体（自定义数据类型）

### 结构体的定义

> ```c
> struct Stu{
>     char name[20];
>     char tele[12];
>     char sex[10];
>     int age;
> }s3,s4;				//创建全局变量s3，s4
> 
> struct Stu s2;		//创建全局变量s2
> 
> int main(){
>     struct Stu s1;	//创建局部变量s1
>     return 0;
> }
> ```



### 匿名结构体类型

> ```C
> struct {
>     char name[20];
>     char tele[12];
>     char sex[10];
>     int age;
> }X;		//创建类型的同时，创建结构体类型的对象
> 
> struct {
>     char name[20];
>     char tele[12];
>     char sex[10];
>     int age;
> }*px;		//创建类型的同时，创建结构体类型的指针
> 
> //但是编译器认为 同时创建的这两个结构体类型 不是同一个所以不能 px = &X ；
> ```



### 结构体的自引用

> - 应用在链表上
>   - 数据域
>   - 指针域
>
> ```c
> struct Node{
>     int data；
>     struct Node* next；
> }；
> ```
>
> ==切记不可==
>
> ```C
> struct Node{
>     int data；
>     struct Node n；
> }；
>    
> //因为无法确定数据大小
> // sizeof(struct Node)
> ```



### 结构体的重命名

> ```c
> typedef struct Node{
>     int data；
>     struct Node* next；
> }Node；
>     
> int main(){
>     struct Node n1;		//类型
>     Node n2;
>     return 0;
> }
> ```
>
> ==切记不可==
>
> ```c
> typedef struct{
>     int data；
>     Node* next；
> }Node；
>     
> //因为 还没创建出Node时，已经在结构体中使用Node了
> ```



### 结构体内存对齐

#### 内存对齐规则

> 1. 第一个成员 ==在与结构体变量偏移量为0== 的地址处.
> 2. 其他成员变量要==对齐到某个数字（对齐数）的整数倍==的地址处。 
>    - 对齐数 = 编译器默认的一个对齐数 与 该成员大小的较小值。
>    -  VS中默认的值为8 
>    - gcc编译器没有默认对齐数
> 3. 结构体总大小为==最大对齐数==（每个成员变量都有一个对齐数）的==整数倍==。
> 4. 如果嵌套了结构体的情况，==嵌套的结构体==对齐到==自己的最大对齐数的整数倍处==，结构体的整体大小就是所有最大对齐数（含嵌套结构体的对齐数）的整数倍。

> 为什么存在内存对齐？
>
> 1. 平台原因(==移植原因==)： 不是所有的硬件平台都能访问任意地址上的任意数据的；某些硬件平台只能在某些地址处取某些特 定类型的数据，否则抛出硬件异常。
> 2. ==性能原因==： 数据结构(尤其是栈)应该尽可能地在自然边界上对齐。 原因在于，为了访问未对齐的内存，处理器需要作两次内存访问；而对齐的内存访问仅需要一次访问。

> ```c
> //练习1
> struct S1  
> {
> 	char c1; //  1  8
> 	int i;	 //  4  8
> 	char c2; //  1  8
> };
> printf("%d\n", sizeof(struct S1));	// 1 8 9 ==> 12
> 
> //练习2
> struct S2
> {
> 	char c1;	//1  8
> 	char c2;	//1  8
> 	int i;		//4  8
> };
> printf("%d\n", sizeof(struct S2));	// 1 2 8 ==> 8
> 
> //练习3
> struct S3
> {
> 	double d;	//8  8
> 	char c;		//1  8
> 	int i;		//4  8
> };
> printf("%d\n", sizeof(struct S3)); // 8 9 16 ==> 16
> 
> //练习4-结构体嵌套问题
> struct S4
> {
> 	char c1;		// 1  8
> 	struct S3 s3;	// 结构体中最大的对齐数8  8
> 	double d;		// 8  8
> };
> printf("%d\n", sizeof(struct S4)); // 1  24  32  ==> 32
> 
> 
> ```



#### 修改内存对齐数

> ```C
> #pragma pack(4)    //设置默认对齐数为4
> struct S{
>     char c;
>     double d;
> }
> #pragma pack() 		//设置为 默认的对齐数
> ```



#### offsetof

> - 头文件 stddef.h
> - 不是函数，是宏
> - 返回的是；该成员变量 相对于 结构体起始位置的 偏移量
>
> ```C
> struct S
> {
> 	double d;	//8  8
> 	char c;		//1  8
> 	int i;		//4  8
> };
> printf("%d\n",offsetof(struct S,d)); //0
> printf("%d\n",offsetof(struct S,c)); //8
> printf("%d\n",offsetof(struct S,i)); //12
> ```



### 结构体传参

> 结构体传参，要用传地址
>
> 1. 函数传参的时候，参数是需要压栈，会有时间和空间上的系统开销。
> 2. 如果传递一个结构体对象的时候，结构体过大，参数压栈的的系统开销比较大，所以会导致性能的下降。
> 3. 如果不想改变结构体的数据，就在形式参数列表用==const==修饰
>
> ```C
> struct S
> {
> 	int data[1000];
> 	int num;
> };
> 
> //结构体传参
> void print1(struct S s)
> {
> 	printf("%d\n", s.num);
> }
> 
> //结构体地址传参
> void print2(struct S* ps)
> {
> 	printf("%d\n", ps->num);
> }
> int main()
> {
>     struct S s = {{1,2,3,4}, 1000};
>     
> 	print1(s);  //传值
> 	print2(&s); //传址
>     
> 	return 0;
> }
> ```



### 位段

> 1. 位段的成员必须是 int、unsigned int 、signed int 等==整型类型==。
> 2. 位段的成员名后边有一个==冒号==和一个==数字==。
>
>  
>
> 1. 位段的成员可以是 int unsigned int signed int 或者是 char （属于整形家族）类型 
> 2. 位段的空间上是按照需要以4个字节（ int ）或者1个字节（ char ）的方式来开辟的。 
> 3. 位段涉及很多不确定因素，位段是==不跨平台==的，注重可移植的程序应该避免使用位段。
> 4. 数据大小==超过开辟空间== 就会报错



> ```C
> struct S
> {
> 	int a:2;		//第一个int空间32个bit位，使用了17个bit 浪费了15个bit
> 	int b:5;		//第二个int空间  放30个bit数据
> 	int c:10;
> 	int d:30;
> };
> int main(){
>     struct S s;
>     printf("%d\n",sizeof(s));	//8
> }
> ```
>
> 从字节左边还是右边开始使用 ？
>
> ==由编译器决定==
>
> ```C
> struct S{			//开了3个字节空间
>     char a : 3;
>     char b : 4;
>     char c : 5;
>     char d : 4;
> };
> int main(){
>     struct S s = { 0 };
>     s.a = 10;		//高位存不下， 只能存二进制 010
>     s.b = 20;		// 0100
>     s.c = 3;		// 00011
>     s.d = 4;		// 0100
> }
> ```



#### 位段跨平台的问题

> 1. int 位段被当成==有符号数还是无符号数==是不确定的。 
> 2. 位段中最大位的数目不能确定。（16位机器最大16，32位机器最大32，写成27，在16位机器会出问题。 
> 3. 位段中的成员在内存中从左向右分配，还是从右向左分配标准尚未定义。 
> 4. 当一个结构包含两个位段，第二个位段成员比较大，无法容纳于第一个位段剩余的位时，是舍弃剩余的位还是利用，这是不确定的。



#### 位段的应用

![image-20230224133923728](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20230224133923728.png)



### 枚举

> 1. 枚举常量默认从0开始

> 枚举的优点（对比define）
>
> 1. 增加代码的可读性和可维护性 
> 2. 和#define定义的标识符比较 ==枚举有类型检查==，==更加严谨==。 
> 3. 防止了命名污染（封装）
> 4. 便于调试 
> 5. 使用方便，一次可以定义多个常量

> ```C
> enum Day//星期
> {
> 	Mon,
> 	Tues,
> 	Wed,
> 	Thur,
> 	Fri,
> 	Sat,
> 	Sun
> };
> 
> ```



### 联合体（共用体）

> - 联合体的成员是共用同一块内存空间的
> - 但是不能同时使用变量
>
> ```C
> //联合类型的声明
> union Un
> {
> 	char c;
> 	int i;
> };
> //联合变量的定义
> union Un un;
> //计算连个变量的大小
> printf("%d\n", sizeof(un));	 //4
> 
> // 下面输出的结果是一样的
> printf("%p\n", &u);
> printf("%p\n", &(un.i));
> printf("%p\n", &(un.c));
> ```

#### 大小端



> ```C
> int main(){
>     int a = 0x11 22 33 44;
>     //低地址-----------------------高地址
>     //...[][][11][22][33][44][][][]...   大端字节序存储模式
>     //...[][][44][33][22][11][][][]...   小端字节序存储模式
> }
> ```

- 判断字节序

> ```C
> int  main(){
>     int a = 1;
>     if( 1 == *(char*)&a){
>         printf("小端");	//数据低位 存在 低地址
>     }
>     else{
>         printf("大端");
>     }
>     return 0;
> }
> ```

- 利用联合体的优势

> ```C
> int check_sys(){
>     union Un{     //也可匿名创建
>         char c;
>         int i;
>     }u;
>     u.i = 1;
>     return u.c;
> }//  返回0大端  返回1小端
> ```



#### 联合体的大小

> - 联合的大小至少是最大成员的大小。
> - 当最大成员大小不是最大对齐数的整数倍的时候，就要==对齐到最大对齐数==的整数倍。

> ```C
> union Un
> {
> 	char c[5];		//对齐数 1  8  ==》  1
> 	int i;			//		4  8  ==》  4
> };
> 
> //最大成员的大小是5 ，不是4的倍数，大小是8
> ```



## 内存分配

### 内存中数据的存储

![image-20230228214251960](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302282143463.png)

![image-20230301130131919](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303011301085.png)



> 1. 栈区（stack）：在执行函数时，函数内局部变量的存储单元都可以在栈上创建，函数执行结 束时这些存储单元自动被释放。栈内存分配运算内置于处理器的指令集中，效率很高，但是 分配的内存容量有限。 栈区主要存放运行函数而分配的局部变量、函数参数、返回数据、返 回地址等。 
> 2. 堆区（heap）：一般由程序员分配释放， 若程序员不释放，程序结束时可能由OS回收 。分 配方式类似于链表。 
> 3. 数据段（静态区）（static）存放全局变量、静态数据。程序结束后由系统释放。 
> 4. 代码段：存放函数体（类成员函数和全局函数）的二进制代码。

### 为什么要有动态内存分配

> C语言不一定支持变长数组，C99标准支持，GCC编译器支持

> 动态内存分配有两个特点
>
> 1. 可以动态开辟空间



### malloc和free

> void* malloc (size_t size);
>
> 头文件：stdlib.h
>
> 参数：==字节数==
>
> 返回值：返回空间的地址

> void free (void* ptr);
>
> 头文件：stdlib.h
>
> 参数：开辟空间的地址

> 如何使用？
>
> ```c
> int * p = (int*)malloc(10 * sizeof(int));
> ```
>
> 如果==开辟失败，返回空指针==
>
> ```c
> if( p == NULL){
>     //打印错误原因
>     printf("%s\n",strerror(error));
> }
> else{
>     //正常使用空间
> }
> ```
>
> 申请的空间不再使用后，==释放空间==
>
> ```c
> free(p);
> p = NULL; //不能藕断丝连
> ```



### calloc

> void* calloc (size_t num, size_t size);
>
> 参数1：元素的个数
>
> 参数2：每个元素的字节数
>
> 返回值：开辟空间的指针
>
> 功能：开辟空间后，==元素初始化为0==



### realloc

> void* realloc (void* ptr,size_t size);
>
> 功能：调整开辟内存空间的大小，追加内存空间
>
> 参数1：需要追加空间的地址
>
> 参数2：追加的字节数
>
> 返回值：==追加后的空间地址==

> realloc注意事项
>
> 1. 如果p指向的空间之后有足够的内存空间可以追加，则直接追加，后返回p
> 2. 如果p指向的空间之后没有足够的内存空间可以追加，则realloc函数会重新找一个新的内存区域开辟一块满足需求的空间，并且把原来内存中的数据拷贝过来，释放旧的内存空间，最后返回新的内存空间地址
> 3. 如果用p接收realloc函数的返回值，若realloc开辟失败，则p被赋值NULL

> 正确使用方法：
>
> ```c
> int * ptr = (int*)realloc(p,INT_MAX);
> if(ptr != NULL){
>  p = ptr;
> }
> //使用完毕后
> free(p);
> p = NULL;
> ```
>
> realloc实现malloc
>
> ```c
> int * p = realloc(NULL,40);
> ```







### 内存操作常见错误

> 1. 开辟地址后，必须进行判断
> 2. 开辟空间后，不能越界访问
> 3. 避免对非动态开辟的内存使用free释放
>
> ```c
> void test()
> {
> 	int i = 0;
> 	int *p = (int *)malloc(10*sizeof(int));
> 	if(NULL == p)
> 	{
> 		exit(EXIT_FAILURE);
> 	}
> 	for(i=0; i<10; i++)
> 	{
> 		*P++ = i;
> 	}
> 	free(p);		//释放的是开辟的内存空间 后面 的空间
> }
> 
> ```
>
> 4. 避免free释放一块动态开辟内存的一部分
>
> ```C
> void test()
> {
> 	int *p = (int *)malloc(100);
>  	p++;
>  	free(p);//p不再指向动态内存的起始位置
> }
> ```
>
> 5.  对同一块动态内存多次释放
>
> ```C
> void test()
> {
> 	int *p = (int *)malloc(100);
> 	free(p);
> 	free(p);  //重复释放  原则：谁申请 谁回收
> }
> ```
>
> 6. 忘记释放开辟的内存（==内存泄漏==）



### 笔试题

> 题目1：
>
> ```c
> void GetMemory(char *p)
> {
> 	p = (char *)malloc(100);	//函数结束后，p找不到了，内存泄漏
> }
> 
> void Test(void)
> {
> 	char *str = NULL;
> 	GetMemory(str);				//传值 实际上str并没有开辟空间
> 	strcpy(str, "hello world");	//空地址不能放数据，程序崩溃
> 	printf(str);
> }
> ```
>
> 如何改进?
>
> 方式1：
>
> ```C
> void GetMemory(char**p)
> {
> 	*p = (char *)malloc(100);
> }
> 
> void Test(void)
> {
> 	char *str = NULL;
> 	GetMemory(&str);				
> 	strcpy(str, "hello world");
> 	printf(str);
>     
>     free(str);
>     str = NULL;
> }
> ```
>
> 方式2：
>
> ```C
> char* GetMemory(char *p)
> {
> 	p = (char *)malloc(100);
>     return p;
> }
> 
> void Test(void)
> {
> 	char *str = NULL;
> 	str = GetMemory(str);		
> 	strcpy(str, "hello world");	
> 	printf(str);
>     
>     free(str);
>     str = NULL;
> }
> 
> ```



> 题目2：
>
> 返回==栈空间的地址==的问题
>
> ```C
> char *GetMemory(void)
> {
> 	char p[] = "hello world";	//函数结束，空间会还给OS
> 	return p;
> }
> 
> void Test(void)
> {
> 	char *str = NULL;
> 	str = GetMemory();
> 	printf(str);
> }
> 
> ```
>
> 类似的
>
> ```C
> int * test()
> {
> 	int a = 10 ;
> 	return &a;
> }
> 
> int main()
> {
> 	int*p = test();
>     *p = 20;
> }
> ```
>
> 但是
>
> ```C
> int * test()
> {
> 	static int a = 10 ;	//a不在栈区 在静态区
> 	return &a;
> }
> 
> int main()
> {
> 	int*p = test();
>     *p = 20;
> }
> ```
>
> ```C
> int * test()
> {
> 	int *ptr = malloc(100);	//ptr虽然被销毁了，但空间地址 传 出去了
> 	return ptr;
> }
> 
> int main()
> {
> 	int*p = test();
> }
> ```

> 题目3：
>
> ```c
> void GetMemory(char **p, int num)
> {
> 	*p = (char *)malloc(num);	//*p 就是外面的 str
> }
> 
> void Test(void)
> {
> 	char *str = NULL;
> 	GetMemory(&str, 100);
>  	strcpy(str, "hello");	//打印hello ， 存在内存泄漏
>  	printf(str);
> }
> 
> ```



> 题目4：
>
> ```C
> void Test(void)
> {
>  	char *str = (char *) malloc(100);
> 	strcpy(str, "hello");
>  	free(str);			//不使用空间后，应该str = NULL
>  	if(str != NULL)
>  	{
> 		strcpy(str, "world");
>  		printf(str);
> 	}
> }
> ```



## 文件操作

### 什么是文件？

> 磁盘上的文件是文件
>
> 在程序设计中，一般谈的文件有两种：程序文件、数据文件

### 程序文件

> 包括源程序文件（后缀为.c）
>
> 目标文件（windows环境后缀为.obj）
>
> 可执行程序（windows环境 后缀为.exe）

### 数据文件

> 文件的内容不一定是程序，而是程序运行时读写的数据，比如程序运行需要从中读取数据的文件或者输出内容的文件

### 文件名

> 一个文件要有一个唯一的文件标识，以便用户识别和引用
>
> 文件名包含3部分：文件路径+文件名主干+文件后缀
>
> 例如： c:\code\test.txt
>
> 为了方便起见，==文件标识==常被称为==文件名==

### 文件类型

> 文件的类型：
>
> - 文本文件
>   - 字符一律以ASCII码形式存储
> - 二进制文件
>   - 数值型数据既可以用ASCII码存储，也可以用二进制形式存储

> 把10000存入内存
>
> ![image-20230303111845934](C:\Users\13192\AppData\Roaming\Typora\typora-user-images\image-20230303111845934.png)

### 文件缓冲区

> 数据放满缓冲区，才一起输入\输出

![image-20230304094718665](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303040947752.png)

### 文件指针

> - 每个被使用的文件都在内存中开辟了一个相应的文件信息区，用来存放文件的相关信息（如==文件的名字==，==文件状态==及==文件当前的位置==等）
>
> - 这些信息是保存在一个==结构体变量中==的。该结构体类型是有系统声明的，取名FILE
>
>   - ```C
>     struct _iobuf {
>             char *_ptr;
>             int   _cnt;
>             char *_base;
>             int   _flag;
>             int   _file;
>             int   _charbuf;
>             int   _bufsiz;
>             char *_tmpfname;
>     };
>     typedef struct _iobuf FILE;
>     ```
>
>   

### 文件打开关闭

```C
//打开文件
FILE * fopen ( const char * filename, const char * mode );
//关闭文件
int fclose ( FILE * stream );
```

> FILE * fopen ( const char * filename, const char * mode );
>
> 参数1：文件名
>
> 参数2：打开模式

> int fclose ( FILE * stream );
>
> 参数：文件流

> 使用方式：
>
> ```C
> //文件打开
> FILE* pf = fopen("test.txt","r");
> if(pf == NULL){
>     printf("%s\n",strerror(errno));
>     return 0;
> }
> //文件使用  ......
> //文件关闭
> fclose(pf);
> pf = NULL;
> 
> ```
>
> 

### 文件打开模式

> 读就是将cpu中的数据送到内存或磁盘
>
> 写就是将内存或磁盘中的数据送入cpu

| 文件使用方式  |                     含义                     | 如果指定文件不存在 |
| :-----------: | :------------------------------------------: | :----------------: |
|  “r”（只读）  | 为了输入数据，打开一个==已经存在==的文本文件 |        出错        |
|  “w”（只写）  |        为了输出数据，打开一个文本文件        |  建立一个新的文件  |
|  “a”（追加）  |             向文本文件尾添加数据             |  建立一个新的文件  |
| “rb”（只读）  |       为了输入数据，打开一个二进制文件       |        出错        |
| “wb”（只写）  |       为了输出数据，打开一个二进制文件       |  建立一个新的文件  |
| “ab”（追加）  |          向一个二进制文件尾添加数据          |        出错        |
| “r+”（读写）  |         为了读和写，打开一个文本文件         |        出错        |
| “w+”（读写）  |         为了读和写，建议一个新的文件         |  建立一个新的文件  |
| "a+”（读写）  |        打开一个文件，在文件尾进行读写        |  建立一个新的文件  |
| "rb+”（读写） |         为了读和写打开一个二进制文件         |        出错        |
| “wb+”（读写） |      为了读和写，新建一个新的二进制文件      |  建立一个新的文件  |
| “ab+”（读写） |    打开一个二进制文件，在文件尾进行读和写    |  建立一个新的文件  |

### 文件函数

|      功能      | 函数名  |   适用于   |
| :------------: | :-----: | :--------: |
|  字符输入函数  |  fgetc  | 所有输入流 |
|  字符输出函数  |  fputc  | 所有输出流 |
| 文本行输入函数 |  fgets  | 所有输入流 |
| 文本行输出函数 |  fputs  | 所有输出流 |
| 格式化输入函数 | fscanf  | 所有输入流 |
| 格式化输出函数 | fprintf | 所有输出流 |
|   二进制输入   |  fread  |    文件    |
|   二进制输出   | fwrite  |    文件    |

> char* fgets(char * string,int n , FILE * stream);
>
> 参数1：读到哪去
>
> 参数2：读几个元素
>
> 参数3：从哪里读
>
> 细节：==文本中换行符也会读入==
>
> 如何使用：
>
> ```C
> char buf[1024] = {0};
> FILE * pf = fopen("test.txt","r");
> if(pf == NULL){
>     return 0;
> }
> fgets(buf,1024,pf);		//文件函数
> printf("%s",buf);
> fclose(pf);
> pf = NULL;
> ```

#### 函数对比

> ![image-20230304152627983](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303041526036.png)
>
> 函数的区别：
>
> 1. printf默认stdout，fprintf更加灵活

![image-20230304160723139](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303041607200.png)

> 字符串和结构体的互动：
>
> ```c
> struct S{
>     int n ;
>     float score;
>     char arr[10];
> };
> int main(){
>     struct S s = {100,3.14f,"abc"};
>     struct S tmp = {0};
>     char buf[1024] = {0};
>     sprintf(buf,"%d %f %s",s.n,s.score,s.arr);				//输出到buf
>     sscanf(buf,"%d %f %s",&(tmp.n),&(tmp.score),tmp.arr);	//将buf数据读入到tmp
>     
> }
> ```

#### 二进制形式

> size_t fwrite(const void * buffer,size_t size, size_t count, FILE * stream);
>
> 参数1：数据从哪来
>
> 参数2：一个数据的大小
>
> 参数3：数据的个数
>
> 参数4：写到哪里去
>
> 返回值：处理的元素个数（如果没处理返回0）

> size_t  fread(const void * buffer,size_t size, size_t count, FILE * stream);
>
> 参数1：数据读到哪里去
>
> 参数2：一个数据的大小
>
> 参数3：数据的个数
>
> 参数4：从哪读数据
>
> 返回值：处理的元素个数（如果没处理返回0）



### 流stream

> 默认打开了两个流设备
>
> 键盘 - 默认输入设备
>
> 屏幕 - 标准输出设备

> 默认打开：
>
> stdin
>
> stdout
>
> stderr

> 使用方式：
>
> ```C
> int ch = fgets(stdin);	//键盘输入
> fputc(ch, stdout);		//屏幕输出
> ```

### 文件的随机读写

#### fseek

> 根据文件指针的位置和偏移量来定位文件指针

> int fseek ( FILE * stream, long int offset, int origin );
>
> 参数1：文件指针
>
> 参数2：偏移量
>
> 参数3：文件指针的当前位置
>
> - SEEK_CUR	文件指针的当前位置
> - SEEK_END     文件的末尾位置
> - SEEK-SET        文件的起始位置

> 如何使用：
>
> ```C
> fssek(pf,2,SEEK_END);
> ```



#### ftell

> 返回文件指针相对于起始位置的偏移量

> long int ftell ( FILE * stream );



#### frewind

> 让文件指针的位置回到文件的起始位置

> void rewind ( FILE * stream );

### 文件结束判定

#### feof

> EOF - end of file 文件结束标志

> 牢记：在文件读取过程中，不能用feof函数的返回值直接用来判断文件的是否结束。
>
> 而是应用于当文件读取结束的时候，判断==是读取失败结束，还是遇到文件尾结束==

#### 处理文本文件

> ```C
> #include <stdio.h>
> #include <stdlib.h>
> int main(void)
> {
>     	int c; // 注意：int，非char，要求处理EOF
>     	FILE* fp = fopen("test.txt", "r");
>     	if(!fp) {
>         	perror("File opening failed");
>         	return EXIT_FAILURE;
>    	}
>  	//fgetc 当读取 失败的时候 或者 遇到文件结束的时候，都会返回EOF
>     	while ((c = fgetc(fp)) != EOF) // 标准C I/O读取文件循环
>    	{ 
>        	putchar(c);
>    	}
>  	//判断是什么原因结束的
>     	if (ferror(fp))					//判断是否读取失败
>         	puts("I/O error when reading");
>     	else if (feof(fp))				//判断是否是碰到文件结束
>         	puts("End of file reached successfully");
>     	 	fclose(fp);
>     	 	fp = NULL;
> }
> ```

#### 处理二进制文件

> ```C
> #include <stdio.h>
> enum { SIZE = 5 };
> int main(void)
> {
>     double a[SIZE] = {1.0, 2.0, 3.0, 4.0, 5.0 };
> 	double b = 0.0;
>     size_t ret_code = 0;
>     FILE *fp = fopen("test.bin", "wb"); // 必须用二进制模式
>     fwrite(a, sizeof *a, SIZE, fp); // 写 double 的数组
>     fclose(fp);
>     
> 
>     fp = fopen("test.bin","rb");
>     // fread返回值为0时，读入完毕
>     while( ret_code == fread(&b, sizeof(double), 1, fp )) >= 1 )
>     {
>         printf("lf\n",b);
>     } 
>     //判断文件结束的原因
>     if (feof(fp))
>          printf("Error reading test.bin: unexpected end of file\n");
>     else if (ferror(fp)) 
>         perror("Error reading test.bin");
>     fclose(fp);
> 	fp = NULL;
> }
> 
> ```
>



## 预处理

![image-20230305232255961](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303052322062.png)

### 预编译

> 执行的功能（文本操作）：
>
> 1. #include
> 2. 注释删除
> 3. #define

### 编译

> 执行的功能：
>
> 1. 语法分析
> 2. 词法分析（编译原理，语法树）
> 3. 语义分析
> 4. 符号汇总

### 汇编

> 执行的功能：
>
> 1. 形成符号表（符号名 和 地址）



### 链接

> 执行的功能：
>
> 1. 合并段表（每个文件都有1个elf文件格式）
> 2. 符号表的合并和重定位（选择有效的符号地址）



### 预定义符号

> ```C
> __FILE__     	 //进行编译的源文件
> __LINE__    	 //文件当前的行号
> __DATE__   	 	 //文件被编译的日期
> __TIME__    	 //文件被编译的时间
> __STDC__    	 //如果编译器遵循ANSI C，其值为1，否则未定义
> __FUNCITON__	 //函数名	
> ```

> ```C
> printf("%s\n",__FILE__); //打印文件名
> ```
>
> ```C
> printf("%s\n",__LINE__); //打印行号
> ```
>
> ```C
> printf("%s\n",__ANSI__); //打印行号
> ```



### 预处理指令

> #开头的指令，都叫预处理指令
>
> ```c
> # define
> #include
> #pragma pack(4)
> #pragame
> #if
> #endif
> #ifdef
> #line
> ```

### 定义标识符

> ```C
> #define reg register
> #define do_forever for(;;)
> #define CASE break;case
> // 如果定义的 stuff过长，可以分成几行写，除了最后一行外，每行的后面都加一个反斜杠(续行符)。
> #define DEBUG_PRINT printf("file:%s\tline:%d\t \
>                           date:%s\ttime:%s\n" ,\
> 							__FILE__,__LINE__ ,\
> 							__DATE__,__TIME__ ) 
> ```



> ```C
> #define do_forever for(;;)
> int main(){
>     do_forever;				//一定要加 ; ，因为不加分号 return 0 会成为for循环的代码块
>     return 0;
> }
> ```



> 在define定义标识符的时候，要不要在最后加上 ; 
>
> ```C
> #define MAX 1000;
> if(condition)
>      max = MAX;
> else
>      max = 0;
> ```
>
> if不加{}只会执行一句代码



> ```C
> #define MAX 1000;
> printf("%d\n",MAX);	
> ```
>
> 语法错误

