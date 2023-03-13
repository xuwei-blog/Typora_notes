# C#面向对象

## 概述

[TOC]



## C# 高阶语法

### 软件开发流程

![image-20230310084550831](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303100845895.png)

### 面向对象三大特性

![image-20230310085249632](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303100852683.png)

### OOP原则

![image-20230310085423127](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303100854183.png)

```
依赖倒置原则，DIP,Dependency Inverse Principle DIP的表述是：

1、高层模块不应该依赖于低层模块, 二者都应该依赖于抽象。

2、抽象不应该依赖于细节,细节应该依赖于抽象。

这里说的“依赖”是使用的意思，如果你调用了一个类的一个方法，就是依赖这个类，如果你直接调用这个类的方法，就是依赖细节，细节就是具体的类，但如果你调用的是它父类或者接口的方法，就是依赖抽象， 所以 DIP 说白了就是不要直接使用具体的子类，而是用它的父类的引用去调用子类的方法，这样就是依赖于抽象，不依赖具体。

其实简单的说，DIP 的好处就是解除耦合，用了 DIP 之后，调用者就不知道被调用的代码是什么，因为调用者拿到的是父类的引用，它不知道具体指向哪个子类的实例，更不知道要调用的方法具体是什么，所以，被调用代码被偷偷换成另一个子类之后，调用者不需要做任何修改， 这就是解耦了。
```



### 封装

> **封装** 被定义为"把一个或多个项目封闭在一个物理的或者逻辑的包中"
>
> 在面向对象程序设计方法论中，封装是为了防止对实现细节的访问
>
> 抽象允许相关信息可视化，封装则使开发者*实现所需级别的抽象*

>  C# 支持的访问修饰符如下所示 :
>
> - public：所有对象都可以访问；
> - private：对象本身在对象内部可以访问；
> - protected：只有该类对象及其子类对象可以访问；
> - internal：同一个程序集的对象可以访问；
> - protected internal：访问限于当前程序集或派生自包含类的类型。

![image-20230310103612256](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303101036284.png)



-  (1) **Pubilc** ：任何公有成员可以被外部的类访问。
-  (2) **Private** ：只有同一个类中的函数可以访问它的私有成员。
-  (3) **Protected** ：该类内部和继承类中可以访问。
-  (4) **internal** : 同一个程序集的对象可以访问。
-  (5) **Protected internal** ：3 和 4 的并集，符合任意一条都可以访问



#### Private 访问修饰符

> Private 访问修饰符允许一个类将其成员变量和成员函数对其他的函数和对象进行隐藏
>
> 只有同一个类中的函数可以访问它的私有成员
>
> 即使是类的实例也不能访问它的私有成员

#### Protected 访问修饰符

> Protected 访问修饰符允许子类访问它的基类的成员变量和成员函数

#### Internal 访问修饰符

> Internal 访问修饰符允许一个类将其成员变量和成员函数暴露给当前程序中的其他函数和对象



#### Protected Internal 访问修饰符

> Protected Internal 访问修饰符允许在本类,派生类或者包含该类的程序集中访问



### 类的定义规范

> 字段：成员变量
>
> - 字段主要是为类的内部做数据交互使用，字段一般是private。
>
>   字段可读可写。
>
>   当字段需要为外部提供数据的时候，请将字段封装为属性，而不是使用公有字段(public修饰符)，这是面向对象思想所提倡的。
>
> 属性：方法
>
> - 属性一般是向外提供数据，主要用来描述对象的静态特征，所以，属性一般是public。
>
>   自动属性具备get和set方法，可以在方法里加入逻辑处理数据，灵活拓展使用。
>
>   ![image-20230312235704272](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303122357309.png)



> **硬编码：** 类中的静态字段，外部无法修改 , 比如使用 **const**关键字

> **const：** 静态常量，是编译时常量，const较高效
> **readonly：** 动态常量，是运行时常量，readonly较灵活

> 1. const默认是静态的，只能由类型来访问，不能与static同时使用；readonly默认是非静态的，由实例对象来访问，可以显示使用static定义为静态成员；
>
> 2. const只能应用在值类型和string类型上，其他引用类型常量只能定义为null，否则以new为const引用类型常量赋值，；readonly只读字段，可以使任意类型，但是对于引用类型字段来说，readonly不能限制对该对象实例成员的读写控制；编译器会引发“只能用null对引用类型（字符串除外）的常量进行初始化“的错误提示；
>
> 3. const必须在字段声明时初始化；readonly可以再声明时，或者构造函数中进行初始化，不同的构造函数可以为readonly常量实现不同的初始值；
>
> 4. const可以定义字段和局部变量；而readonly则只能定义字段；static readonly的初始化，必须在定义时，或者静态无参构造函数中进行；
>
> 5. 数组和结构体不能被声明为const常量，string类型可以被声明为常量，因为string类型的字符串恒定特性，使得string的值具有只读特性；



![image-20230310085845538](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303100858606.png)

#### 类的定义

```C#
namespace test1
{
    class Program
    {
        static void Main(string[] args)
        {
            //创建对象
            Student objStudent = new Student();
            //给对象赋值
            objStudent.StudentId = 10001;
            objStudent.StudentName = "zhangsan";
            //调用对象方法
            string info = objStudent.GetStudent();
            Console.WriteLine(info);
            Console.ReadLine();
        }
    }
}
```

```C#
namespace test1
{
    class Student
    {
        //字段
        private int studentId;
        private string studentName = string.Empty;
        //属性
        public int StudentId
        {
            get { return studentId; }
            set { studentId = value; }
        }
        public string StudentName
        {
            get { return studentName; }
            set { studentName = value; }
        }
        //方法
        public string GetStudent()
        {
            string info = string.Format("name:{0} id:{1}", studentName, studentId);
            return info;
        }
    }
}
```

#### 定义方法

> 每一个 C# 程序至少有一个带有 Main 方法的类

```C#
<Access Specifier> <Return Type> <Method Name>(Parameter List)
{
   Method Body
}
```

下面是方法的各个元素：

- **Access Specifier**：访问修饰符，这个决定了变量或方法对于另一个类的可见性。
- **Return type**：返回类型，一个方法可以返回一个值。返回类型是方法返回的值的数据类型。如果方法不返回任何值，则返回类型为 **void**。
- **Method name**：方法名称，是一个唯一的标识符，且是大小写敏感的。它不能与类中声明的其他标识符相同。
- **Parameter list**：参数列表，使用圆括号括起来，该参数是用来传递和接收方法的数据。参数列表是指方法的参数类型、顺序和数量。参数是可选的，也就是说，一个方法可能不包含参数。
- **Method body**：方法主体，包含了完成任务所需的指令集。

### static关键字

> 程序一旦载入内存，静态成员都会一起被载入内存
>
> static可以修饰类、方法、成员变量，修饰后称为：静态类、静态方法、静态字段

> 使用细节：
>
> 静态成员在程序运行时被调入内存，并且在系统未关闭之前不会被GC回收
>
> 类的成员使用非常频繁的时候，可以考虑用static修饰，但不要过多使用
>
> 静态成员不能直接调用实例成员（静态方法不能直接调用实例方法）

### 参数传递

> 三种向方法传递参数的方式

| 方式     | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| 值参数   | 这种方式复制参数的实际值给函数的形式参数，实参和形参使用的是两个不同内存中的值。在这种情况下，当形参的值发生改变时，不会影响实参的值，从而保证了实参数据的安全。 |
| 引用参数 | 这种方式复制参数的内存位置的引用给形式参数。这意味着，当形参的值发生改变时，同时也改变实参的值。 |
| 输出参数 | 这种方式可以返回多个值。                                     |

#### 值传递

> 参数传递的默认方式
>
> 在这种方式下，当调用一个方法时，会为每个值参数创建一个新的存储位置
>
> 实际参数的值会复制给形参，实参和形参使用的是两个不同内存中的值
>
> 当形参的值发生改变时，不会影响实参的值，从而保证了实参数据的安全

#### 引用传参

> 引用参数是一个对变量的**内存位置的引用**
>
> 当按引用传递参数时，与值参数不同的是，它不会为这些参数创建一个新的存储位置
>
> 引用参数表示与提供给方法的实际参数具有相同的内存位置
>
> 使用 **ref** 关键字声明引用参数

```C#
using System;
namespace CalculatorApplication
{
   class NumberManipulator
   {
      public void swap(ref int x, ref int y)
      {
         int temp;

         temp = x; /* 保存 x 的值 */
         x = y;    /* 把 y 赋值给 x */
         y = temp; /* 把 temp 赋值给 y */
       }
   
      static void Main(string[] args)
      {
         NumberManipulator n = new NumberManipulator();
         /* 局部变量定义 */
         int a = 100;
         int b = 200;

         Console.WriteLine("在交换之前，a 的值： {0}", a);
         Console.WriteLine("在交换之前，b 的值： {0}", b);

         /* 调用函数来交换值 */
         n.swap(ref a, ref b);

         Console.WriteLine("在交换之后，a 的值： {0}", a);
         Console.WriteLine("在交换之后，b 的值： {0}", b);
 
         Console.ReadLine();

      }
   }
}
```

#### 按输出传递参数

> 可以使用 **输出参数** 来从函数中返回两个值
>
> 关键字out，实现2个返回值，功能和泛型类似
>
> 当需要从一个参数没有指定初始值的方法中返回值时，输出参数特别有用

```C#
using System;

namespace CalculatorApplication
{
   class NumberManipulator
   {
      public void getValue(out int x )
      {
         int temp = 5;
         x = temp;
      }
   
      static void Main(string[] args)
      {
         NumberManipulator n = new NumberManipulator();
         /* 局部变量定义 */
         int a = 100;
         
         Console.WriteLine("在方法调用之前，a 的值： {0}", a);
         
         /* 调用函数来获取值 */
         n.getValue(out a);

         Console.WriteLine("在方法调用之后，a 的值： {0}", a);
         Console.ReadLine();

      }
   }
}
//在方法调用之前，a 的值： 100
//在方法调用之后，a 的值： 5
```

```C#
using System;

namespace CalculatorApplication
{
   class NumberManipulator
   {
      public void getValues(out int x, out int y )
      {
          Console.WriteLine("请输入第一个值： ");
          x = Convert.ToInt32(Console.ReadLine());
          Console.WriteLine("请输入第二个值： ");
          y = Convert.ToInt32(Console.ReadLine());
      }
   
      static void Main(string[] args)
      {
         NumberManipulator n = new NumberManipulator();
         /* 局部变量定义 */
         int a , b;
         
         /* 调用函数来获取值 */
         n.getValues(out a, out b);

         Console.WriteLine("在方法调用之后，a 的值： {0}", a);
         Console.WriteLine("在方法调用之后，b 的值： {0}", b);
         Console.ReadLine();
      }
   }
}
//请输入第一个值：
//7
//请输入第二个值：
//8
//在方法调用之后，a 的值： 7
//在方法调用之后，b 的值： 8
```

### 单问号 ? 与 双问号 ??

> **?** 单问号用于对 **int、double、bool** 等无法直接赋值为 null 的数据类型进行 null 的赋值
>
> 意思是这个数据类型是 Nullable 类型的。

```C#
int i; //默认值0
int? ii; //默认值null
```

#### 可空类型（Nullable）

> 特殊的数据类型，**nullable** 类型（可空类型）
>
> 可空类型可以表示其基础值类型正常范围内的值，再加上一个 null 值
>
> 例如，Nullable< Int32 >，读作"可空的 Int32"，可以被赋值为 -2,147,483,648 到 2,147,483,647 之间的任意值
>
> 也可以被赋值为 null 值
>
> 例如，Nullable< bool > 变量可以被赋值为 true 或 false 或 null
>
> 在==处理数据库==和其他包含可能未赋值的元素的数据类型时，将 null 赋值给数值类型或布尔型的功能特别有用

#### Null 合并运算符（ ?? ）

> Null 合并运算符用于定义可空类型和引用类型的默认值
>
> Null 合并运算符为类型转换定义了一个预设值，以防可空类型的值为 Null
>
> Null 合并运算符把操作数类型隐式转换为另一个可空（或不可空）的值类型的操作数的类型
>
> 如果第一个操作数的值为 null，则运算符返回第二个操作数的值，否则返回第一个操作数的值

```C#
using System;
namespace CalculatorApplication
{
   class NullablesAtShow
   {
         
      static void Main(string[] args)
      {
         
         double? num1 = null;
         double? num2 = 3.14157;
         double num3;
         num3 = num1 ?? 5.34;      // num1 如果为空值则返回 5.34
         Console.WriteLine("num3 的值： {0}", num3);
         num3 = num2 ?? 5.34;
         Console.WriteLine("num3 的值： {0}", num3);
         Console.ReadLine();

      }
   }
}
//num3 的值： 5.34
//num3 的值： 3.14157
```

### 数组

> 数组是一个存储相同类型元素的固定大小的顺序集合
>
> 数组是一个同一类型变量的集合

![image-20230310164425179](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303101644236.png)

#### 声明数组

- *datatype* 用于指定被存储在数组中的元素的类型。
- *[ ]* 指定数组的秩（维度）。秩指定数组的大小。
- *arrayName* 指定数组的名称。

```c#
datatype[] arrayName;
```

#### 初始化数组

```C#
double[] balance = new double[10];
```

#### 赋值数组

> 可以通过使用索引号赋值给一个单独的数组元素
>
> ```C#
> double[] balance = new double[10];
> balance[0] = 4500.0;
> ```

> 可以在声明数组的同时给数组赋值
>
> ```C#
> double[] balance = { 2340.0, 4523.69, 3421.0};
> ```

> 可以创建并初始化一个数组
>
> ```C#
> int [] marks = new int[5]  { 99,  98, 92, 97, 95};
> ```

> 可以省略数组的大小
>
> ```C#
> int [] marks = new int[]  { 99,  98, 92, 97, 95};
> ```

> 可以赋值一个数组变量到另一个目标数组变量中 ,在这种情况下,目标和源会指向相同的内存位置
>
> ```C#
> int [] marks = new int[]  { 99,  98, 92, 97, 95};
> int[] score = marks;
> ```

> 创建一个数组时，C# 编译器会根据数组类型隐式初始化每个数组元素为一个默认值
>
> 例如，int 数组的所有元素都会被初始化为 0

#### 访问数组元素

> 元素是通过带索引的数组名称来访问的
>
> 这是通过把元素的索引放置在数组名称后的方括号中来实现的
>
> ```C#
> double salary = balance[9];
> ```

####  *foreach* 循环

>  **foreach** 语句来遍历数组
>
> ```C#
>         //数组n	 
> 		 foreach (int j in n )
>          {
>             int i = j-100;
>             Console.WriteLine("Element[{0}] = {1}", i, j);
>          }
> ```
>
> 

#### 数组细节

| 概念           | 描述                                                         |
| :------------- | :----------------------------------------------------------- |
| 多维数组       | C# 支持多维数组。多维数组最简单的形式是二维数组。            |
| 交错数组       | C# 支持交错数组，即数组的数组。                              |
| 传递数组给函数 | 您可以通过指定不带索引的数组名称来给函数传递一个指向数组的指针。 |
| 参数数组       | 这通常用于传递未知数量的参数给函数。                         |
| Array 类       | 在 System 命名空间中定义，是所有数组的基类，并提供了各种用于数组的属性和方法。 |

##### 多维数组

> 多维数组又称为矩形数组

>  声明一个 string 变量的二维数组
>
> ```C#
> string [,] names;
> ```

> 可以声明一个 int 变量的三维数组
>
> ```C#
> int [ , , ] m;
> ```

###### 二维数组

> 数组中的每个元素是使用形式为 a[ i , j ] 的元素名称来标识的
>
> 其中 a 是数组名称，i 和 j 是唯一标识 a 中每个元素的下标

![image-20230310170656759](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303101706799.png)



> 初始化二维数组
>
> 多维数组可以通过在括号内为每行指定值来进行初始化
>
> 下面是一个带有 3 行 4 列的数组。
>
> ```
> int [,] a = new int [3,4] {
>  {0, 1, 2, 3} ,   /*  初始化索引号为 0 的行 */
>  {4, 5, 6, 7} ,   /*  初始化索引号为 1 的行 */
>  {8, 9, 10, 11}   /*  初始化索引号为 2 的行 */
> };
> ```

###### 交错数组

> 交错数组是数组的数组
>
> 交错数组是一维数组
>
> 您可以声明一个带有 **int** 值的交错数组 *scores*
>
> ```C#
> int [][] scores;
> ```

> 声明一个数组不会在内存中创建数组
>
> ```C#
> int[][] scores = new int[5][];
> for (int i = 0; i < scores.Length; i++) 
> {
>    scores[i] = new int[4];
> }
> ```

> 初始化一个交错数组
>
> scores 是一个由两个整型数组组成的数组 
>
> scores[0] 是一个带有 3 个整数的数组
>
> scores[1] 是一个带有 4 个整数的数组
>
> ```C#
> int[][] scores = new int[2][]{new int[]{92,93,94},new int[]{85,66,87,88}};
> ```

###### 传递数组给函数

> 通过指定不带索引的数组名称来给函数传递一个指向数组的指针

###### 参数数组

> 参数数组通常用于传递未知数量的参数给函数

> 在使用数组作为形参时，C# 提供了 params 关键字，使调用数组为形参的方法时，既可以传递数组实参，也可以传递一组数组元素。params 的使用格式为：
>
> ```
> public 返回类型 方法名称( params 类型名称[] 数组名称 )
> ```

###### Array 类

> Array 类是 C# 中所有数组的基类，它是在 System 命名空间中定义
>
> Array 类提供了各种用于数组的属性和方法

- Array类的属性

| 序号 | 属性 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **IsFixedSize** 获取一个值，该值指示数组是否带有固定大小。   |
| 2    | **IsReadOnly** 获取一个值，该值指示数组是否只读。            |
| 3    | **Length** 获取一个 32 位整数，该值表示所有维度的数组中的元素总数。 |
| 4    | **LongLength** 获取一个 64 位整数，该值表示所有维度的数组中的元素总数。 |
| 5    | **Rank** 获取数组的秩（维度）。                              |

- Array类的方法

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **Clear** 根据元素的类型，设置数组中某个范围的元素为零、为 false 或者为 null。 |
| 2    | **Copy(Array, Array, Int32)** 从数组的第一个元素开始复制某个范围的元素到另一个数组的第一个元素位置。长度由一个 32 位整数指定。 |
| 3    | **CopyTo(Array, Int32)** 从当前的一维数组中复制所有的元素到一个指定的一维数组的指定索引位置。索引由一个 32 位整数指定。 |
| 4    | **GetLength** 获取一个 32 位整数，该值表示指定维度的数组中的元素总数。 |
| 5    | **GetLongLength** 获取一个 64 位整数，该值表示指定维度的数组中的元素总数。 |
| 6    | **GetLowerBound** 获取数组中指定维度的下界。                 |
| 7    | **GetType** 获取当前实例的类型。从对象（Object）继承。       |
| 8    | **GetUpperBound** 获取数组中指定维度的上界。                 |
| 9    | **GetValue(Int32)** 获取一维数组中指定位置的值。索引由一个 32 位整数指定。 |
| 10   | **IndexOf(Array, Object)** 搜索指定的对象，返回整个一维数组中第一次出现的索引。 |
| 11   | **Reverse(Array)** 逆转整个一维数组中元素的顺序。            |
| 12   | **SetValue(Object, Int32)** 给一维数组中指定位置的元素设置值。索引由一个 32 位整数指定。 |
| 13   | **Sort(Array)** 使用数组的每个元素的 IComparable 实现来排序整个一维数组中的元素。 |
| 14   | **ToString** 返回一个表示当前对象的字符串。从对象（Object）继承。 |

### 字符串（String）

> 使用字符数组来表示字符串
>
> 更常见的做法是使用 **string** 关键字来声明一个字符串变量
>
> string 关键字是 **System.String** 类的别名

#### 创建String对象

> 可以使用以下方法之一来创建 string 对象：
>
> - 通过给 String 变量指定一个字符串
> - 通过使用 String 类构造函数
> - 通过使用字符串串联运算符（ + ）
> - 通过检索属性或调用一个返回字符串的方法
> - 通过格式化方法来转换一个值或对象为它的字符串表示形式

> ```C#
> using System;
> 
> namespace StringApplication
> {
>     class Program
>     {
>         static void Main(string[] args)
>         {
>            //字符串，字符串连接
>             string fname, lname;
>             fname = "Rowan";
>             lname = "Atkinson";
> 
>             string fullname = fname + lname;
>             Console.WriteLine("Full Name: {0}", fullname);
> 
>             //通过使用 string 构造函数
>             char[] letters = { 'H', 'e', 'l', 'l','o' };
>             string greetings = new string(letters);
>             Console.WriteLine("Greetings: {0}", greetings);
> 
>             //方法返回字符串
>             string[] sarray = { "Hello", "From", "Tutorials", "Point" };
>             string message = String.Join(" ", sarray);
>             Console.WriteLine("Message: {0}", message);
> 
>             //用于转化值的格式化方法
>             DateTime waiting = new DateTime(2012, 10, 10, 17, 58, 1);
>             string chat = String.Format("Message sent at {0:t} on {0:D}",
>             waiting);
>             Console.WriteLine("Message: {0}", chat);
>             Console.ReadKey() ;
>         }
>     }
> }
> ```
>
> ```
> Full Name: RowanAtkinson
> Greetings: Hello
> Message: Hello From Tutorials Point
> Message: Message sent at 17:58 on Wednesday, 10 October 2012
> ```

#### String 类的属性

| 序号 | 属性名称 & 描述                                              |
| :--- | :----------------------------------------------------------- |
| 1    | **Chars** 在当前 *String* 对象中获取 *Char* 对象的指定位置。 |
| 2    | **Length** 在当前的 *String* 对象中获取字符数。              |

#### String 类的方法

| 序号 | 方法名称 & 描述                                              |
| :--- | :----------------------------------------------------------- |
| 1    | **public static int Compare( string strA, string strB )** 比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。该方法区分大小写。 |
| 2    | **public static int Compare( string strA, string strB, bool ignoreCase )** 比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。但是，如果布尔参数为真时，该方法不区分大小写。 |
| 3    | **public static string Concat( string str0, string str1 )** 连接两个 string 对象。 |
| 4    | **public static string Concat( string str0, string str1, string str2 )** 连接三个 string 对象。 |
| 5    | **public static string Concat( string str0, string str1, string str2, string str3 )** 连接四个 string 对象。 |
| 6    | **public bool Contains( string value )** 返回一个表示指定 string 对象是否出现在字符串中的值。 |
| 7    | **public static string Copy( string str )** 创建一个与指定字符串具有相同值的新的 String 对象。 |
| 8    | **public void CopyTo( int sourceIndex, char[] destination, int destinationIndex, int count )** 从 string 对象的指定位置开始复制指定数量的字符到 Unicode 字符数组中的指定位置。 |
| 9    | **public bool EndsWith( string value )** 判断 string 对象的结尾是否匹配指定的字符串。 |
| 10   | **public bool Equals( string value )** 判断当前的 string 对象是否与指定的 string 对象具有相同的值。 |
| 11   | **public static bool Equals( string a, string b )** 判断两个指定的 string 对象是否具有相同的值。 |
| 12   | **public static string Format( string format, Object arg0 )** 把指定字符串中一个或多个格式项替换为指定对象的字符串表示形式。 |
| 13   | **public int IndexOf( char value )** 返回指定 Unicode 字符在当前字符串中第一次出现的索引，索引从 0 开始。 |
| 14   | **public int IndexOf( string value )** 返回指定字符串在该实例中第一次出现的索引，索引从 0 开始。 |
| 15   | **public int IndexOf( char value, int startIndex )** 返回指定 Unicode 字符从该字符串中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。 |
| 16   | **public int IndexOf( string value, int startIndex )** 返回指定字符串从该实例中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。 |
| 17   | **public int IndexOfAny( char[] anyOf )** 返回某一个指定的 Unicode 字符数组中任意字符在该实例中第一次出现的索引，索引从 0 开始。 |
| 18   | **public int IndexOfAny( char[] anyOf, int startIndex )** 返回某一个指定的 Unicode 字符数组中任意字符从该实例中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。 |
| 19   | **public string Insert( int startIndex, string value )** 返回一个新的字符串，其中，指定的字符串被插入在当前 string 对象的指定索引位置。 |
| 20   | **public static bool IsNullOrEmpty( string value )** 指示指定的字符串是否为 null 或者是否为一个空的字符串。 |
| 21   | **public static string Join( string separator, string[] value )** 连接一个字符串数组中的所有元素，使用指定的分隔符分隔每个元素。 |
| 22   | **public static string Join( string separator, string[] value, int startIndex, int count )** 连接一个字符串数组中的指定位置开始的指定元素，使用指定的分隔符分隔每个元素。 |
| 23   | **public int LastIndexOf( char value )** 返回指定 Unicode 字符在当前 string 对象中最后一次出现的索引位置，索引从 0 开始。 |
| 24   | **public int LastIndexOf( string value )** 返回指定字符串在当前 string 对象中最后一次出现的索引位置，索引从 0 开始。 |
| 25   | **public string Remove( int startIndex )** 移除当前实例中的所有字符，从指定位置开始，一直到最后一个位置为止，并返回字符串。 |
| 26   | **public string Remove( int startIndex, int count )** 从当前字符串的指定位置开始移除指定数量的字符，并返回字符串。 |
| 27   | **public string Replace( char oldChar, char newChar )** 把当前 string 对象中，所有指定的 Unicode 字符替换为另一个指定的 Unicode 字符，并返回新的字符串。 |
| 28   | **public string Replace( string oldValue, string newValue )** 把当前 string 对象中，所有指定的字符串替换为另一个指定的字符串，并返回新的字符串。 |
| 29   | **public string[] Split( params char[] separator )** 返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。 |
| 30   | **public string[] Split( char[] separator, int count )** 返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。int 参数指定要返回的子字符串的最大数目。 |
| 31   | **public bool StartsWith( string value )** 判断字符串实例的开头是否匹配指定的字符串。 |
| 32   | **public char[] ToCharArray()** 返回一个带有当前 string 对象中所有字符的 Unicode 字符数组。 |
| 33   | **public char[] ToCharArray( int startIndex, int length )** 返回一个带有当前 string 对象中所有字符的 Unicode 字符数组，从指定的索引开始，直到指定的长度为止。 |
| 34   | **public string ToLower()** 把字符串转换为小写并返回。       |
| 35   | **public string ToUpper()** 把字符串转换为大写并返回。       |
| 36   | **public string Trim()** 移除当前 String 对象中的所有前导空白字符和后置空白字符。 |

#### 格式化日期

```C#
DateTime dt = new DateTime(2017,4,1,13,16,32,108);
string.Format("{0:y yy yyy yyyy}",dt); //17 17 2017 2017
string.Format("{0:M MM MMM MMMM}", dt);//4  04 四月 四月
string.Format("{0:d dd ddd dddd}", dt);//1  01 周六 星期六
string.Format("{0:t tt}", dt);//下 下午
string.Format("{0:H HH}", dt);//13 13
string.Format("{0:h hh}", dt);//1  01
string.Format("{0:m mm}", dt);//16 16
string.Format("{0:s ss}", dt);//32 32
string.Format("{0:F FF FFF FFFF FFFFF FFFFFF FFFFFFF}", dt);//1 1  108 108  108   108    108
string.Format("{0:f ff fff ffff fffff ffffff fffffff}", dt);//1 10 108 1080 10800 108000 1080000
string.Format("{0:z zz zzz}", dt);//+8 +08 +08:00

string.Format("{0:yyyy/MM/dd HH:mm:ss.fff}",dt);　　//2017/04/01 13:16:32.108
string.Format("{0:yyyy/MM/dd dddd}", dt);　　　　　　//2017/04/01 星期六
string.Format("{0:yyyy/MM/dd dddd tt hh:mm}", dt); //2017/04/01 星期六 下午 01:16
string.Format("{0:yyyyMMdd}", dt);　　　　　　　　　//20170401
string.Format("{0:yyyy-MM-dd HH:mm:ss.fff}", dt);　//2017-04-01 13:16:32.108
```

> 除去string.Format()可以对日期进行格式化之外，*.ToString()也可以实现相同的效果：

```c#
DateTime dt = new DateTime(2017,4,1,13,16,32,108);
dt.ToString("y yy yyy yyyy");//17 17 2017 2017
dt.ToString("M MM MMM MMMM");//4  04 四月 四月
dt.ToString("d dd ddd dddd");//1  01 周六 星期六
dt.ToString("t tt");//下 下午
dt.ToString("H HH");//13 13
dt.ToString("h hh");//1  01
dt.ToString("m mm");//16 16
dt.ToString("s ss");//32 32
dt.ToString("F FF FFF FFFF FFFFF FFFFFF FFFFFFF");//1 1  108 108  108   108    108
dt.ToString("f ff fff ffff fffff ffffff fffffff");//1 10 108 1080 10800 108000 1080000
dt.ToString("z zz zzz");//+8 +08 +08:00

dt.ToString("yyyy/MM/dd HH:mm:ss.fff");　//2017/04/01 13:16:32.108
dt.ToString("yyyy/MM/dd dddd");　　　　　　//2017/04/01 星期六
dt.ToString("yyyy/MM/dd dddd tt hh:mm"); //2017/04/01 星期六 下午 01:16
dt.ToString("yyyyMMdd");　　　　　　　　　//20170401
dt.ToString("yyyy-MM-dd HH:mm:ss.fff");　//2017-04-01 13:16:32.108
```

### 结构体

> 结构体是值类型数据结构
>
> **struct** 关键字用于创建结构体

> 假设想跟踪图书馆中书的动态:
>
> - Title
> - Author
> - Subject
> - Book ID

#### 定义结构体

```C#
struct Books
{
   public string title;
   public string author;
   public string subject;
   public int book_id;
};  
```

#### 结构体的特点

> C# 中的结构与传统的 C 或 C++ 中的结构不同
>
> 结构 指的就是 结构体

- 结构可带有方法、字段、索引、属性、运算符方法和事件。
- 结构可定义构造函数，但不能定义析构函数。但是，不能为结构定义无参构造函数。无参构造函数(默认)是自动定义的，且不能被改变。
- 与类不同，结构不能继承其他的结构或类。
- 结构不能作为其他结构或类的基础结构。
- 结构可实现一个或多个接口。
- 结构成员不能指定为 abstract、virtual 或 protected。
- 当您使用 **New** 操作符创建一个结构对象时，会调用适当的构造函数来创建结构。与类不同，结构可以不使用 New 操作符即可被实例化。
- 如果不使用 New 操作符，只有在所有的字段都被初始化之后，字段才被赋值，对象才被使用。

#### 类和结构的区别

- 类是引用类型，结构是值类型。
- 结构不支持继承。
- 结构不能声明默认的构造函数。

### 枚举

> 枚举是一组命名整型常量
>
> 枚举类型是使用 **enum** 关键字声明的
>
> C# 枚举是值类型
>
> 枚举包含自己的值，且不能继承或传递继承

#### 声明enum变量

声明枚举的一般语法：

```
enum <enum_name>
{ 
    enumeration list 
};
```

其中，

- *enum_name* 指定枚举的类型名称。
- *enumeration list* 是一个用逗号分隔的标识符列表。

枚举列表中的每个符号代表一个整数值，一个比它前面的符号大的整数值。默认情况下，第一个枚举符号的值是 0.例如：

```
enum Days { Sun, Mon, tue, Wed, thu, Fri, Sat };
```

#### 实例

> 实例演示了枚举变量的用法

```C#
using System;

public class EnumTest
{
    enum Day { Sun, Mon, Tue, Wed, Thu, Fri, Sat };

    static void Main()
    {
        int x = (int)Day.Sun;
        int y = (int)Day.Fri;
        Console.WriteLine("Sun = {0}", x);
        Console.WriteLine("Fri = {0}", y);
    }
}
```

结果如下：

```
Sun = 0
Fri = 5
```

## 面向对象核心

### 类（Class）

> 当你定义一个类时，你定义了一个数据类型的蓝图
>
> 这实际上并没有定义任何的数据，但它定义了类的名称意味着什么
>
> 对象是类的实例
>
> 构成类的方法和变量称为类的成员

### 类的定义

>  类的定义是以关键字 class 开始，后跟类的名称
>
> 类的主体，包含在一对花括号内
>
> 下面是类定义的一般形式：
>
> ```C#
> <access specifier> class  class_name
> {
>     // member variables
>     <access specifier> <data type> variable1;
>     <access specifier> <data type> variable2;
>     ...
>     <access specifier> <data type> variableN;
>     // member methods
>     <access specifier> <return type> method1(parameter_list)
>     {
>         // method body
>     }
>     <access specifier> <return type> method2(parameter_list)
>     {
>         // method body
>     }
>     ...
>     <access specifier> <return type> methodN(parameter_list)
>     {
>         // method body
>     }
> }
> ```
>
> 注意：
>
> - 访问标识符 <access specifier> 指定了对类及其成员的访问规则。如果没有指定，则使用默认的访问标识符。类的默认访问标识符是 **internal**，成员的默认访问标识符是 **private**。
> - 数据类型 <data type> 指定了变量的类型，返回类型 <return type> 指定了返回的方法返回的数据类型。
> - 如果要访问类的成员，你要使用点（.）运算符。
> - 点运算符链接了对象的名称和成员的名称。

### 成员函数和封装

> 类的成员函数是一个在类定义中有它的定义或原型的函数，就像其他变量一样
>
> 作为类的一个成员，它能在类的任何对象上操作，且能访问该对象的类的所有成员
>
> 成员变量是对象的属性（从设计角度）

### C# 中的构造函数

> 类的 **构造函数** 是类的一个特殊的成员函数，当创建类的新对象时执行
>
> 构造函数的名称与类的名称完全相同，它没有任何返回类型

> **默认的构造函数**没有任何参数，如果自己写了构造函数，则不会自动生成默认构造
>
> 但是如果需要一个带有参数的构造函数可以有参数，这种构造函数叫做**参数化构造函数**
>
> 这种技术可以在创建对象的同时给对象赋初始值
>
> ```C#
> using System;
> namespace LineApplication
> {
>    class Line
>    {
>       private double length;   // 线条的长度
>       public Line(double len)  // 参数化构造函数
>       {
>          Console.WriteLine("对象已创建，length = {0}", len);
>          length = len;
>       }
> 
>       public void setLength( double len )
>       {
>          length = len;
>       }
>       public double getLength()
>       {
>          return length;
>       }
> 
>       static void Main(string[] args)
>       {
>          Line line = new Line(10.0);
>          Console.WriteLine("线条的长度： {0}", line.getLength());
>          // 设置线条长度
>          line.setLength(6.0);
>          Console.WriteLine("线条的长度： {0}", line.getLength());
>          Console.ReadKey();
>       }
>    }
> }
> ```

#### 构造函数的复用

![image-20230313122646409](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303131226464.png)

### this关键字

> 当成员变量和局部变量重名时使用this区分，this指代成员变量
>
> this表示当前类的对象，用于访问该类成员变量或方法

### 对象初始化器

![image-20230313132958145](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303131329222.png)

### 垃圾回收机制GC

> .NET虚拟机特有机制，自动运行，并检查对象的状态
>
> 发现对象不再引用时，会将其释放所占用的空间（销毁）

### C# 中的析构函数

> 类的 **析构函数** 是类的一个特殊的成员函数，当类的对象超出范围时执行
>
> 析构函数的名称是在类的名称前加上一个波浪形（~）作为前缀，它不返回值，也不带任何参数
>
> 析构函数用于在结束程序（比如关闭文件、释放内存等）之前释放资源
>
> 析构函数不能继承或重载
>
> ```C#
> using System;
> namespace LineApplication
> {
>    class Line
>    {
>       private double length;   // 线条的长度
>       public Line()  // 构造函数
>       {
>          Console.WriteLine("对象已创建");
>       }
>       ~Line() //析构函数
>       {
>          Console.WriteLine("对象已删除");
>       }
> 
>       public void setLength( double len )
>       {
>          length = len;
>       }
>       public double getLength()
>       {
>          return length;
>       }
> 
>       static void Main(string[] args)
>       {
>          Line line = new Line();
>          // 设置线条长度
>          line.setLength(6.0);
>          Console.WriteLine("线条的长度： {0}", line.getLength());          
>       }
>    }
> }
> ```

### C# 类的静态成员

> 我们可以使用 **static** 关键字把类成员定义为静态的
>
> 当我们声明一个类成员为静态时，意味着无论有多少个类的对象被创建，只会有一个该静态成员的副本
>
> 关键字 **static** 意味着类中只有一个该成员的实例
>
> 静态变量用于定义常量，因为它们的值可以通过直接调用类而不需要创建类的实例来获取
>
> 静态变量可在成员函数或类的定义外部进行初始化
>
> 你也可以在类的定义内部初始化静态变量

> 可以把一个**成员函数**声明为 **static** , 这样的函数只能访问静态变量
>
> 静态函数在对象被创建之前就==已经存在==
>
> ```C#
> using System;
> namespace StaticVarApplication
> {
>     class StaticVar
>     {
>        public static int num;
>         public void count()
>         {
>             num++;
>         }
>         public static int getNum()
>         {
>             return num;
>         }
>     }
>     class StaticTester
>     {
>         static void Main(string[] args)
>         {
>             StaticVar s = new StaticVar();
>             s.count();
>             s.count();
>             s.count();                  
>             Console.WriteLine("变量 num： {0}", StaticVar.getNum());	//类名.方法()
>             Console.ReadKey();
>         }
>     }
> }
> ```



### 继承

> 当创建一个类时，不需要完全重新编写新的数据成员和成员函数，只需要设计一个新的类，继承了已有的类的成员即可。这个已有的类被称为的**基类**，这个新的类被称为**派生类**。
>
> 继承的思想实现了 **属于（IS-A）** 关系

#### 基类和派生类

> 一个类可以派生自多个类或接口，这意味着它可以从多个基类或接口继承数据和函数

> 创建派生类的语法：
>
> ```C#
> <访问修饰符> class <基类>
> {
>  ...
> }
> class <派生类> : <基类>
> {
>  ...
> }
> ```



#### 基类的初始化

> 派生类继承了基类的成员变量和成员方法,因此父类对象应在子类对象创建之前被创建
>
> 在成员初始化列表中进行父类的初始化
>
> ```C#
> using System;
> namespace RectangleApplication
> {
>    class Rectangle
>    {
>       // 成员变量
>       protected double length;
>       protected double width;
>       public Rectangle(double l, double w)
>       {
>          length = l;
>          width = w;
>       }
>       public double GetArea()
>       {
>          return length * width;
>       }
>       public void Display()
>       {
>          Console.WriteLine("长度： {0}", length);
>          Console.WriteLine("宽度： {0}", width);
>          Console.WriteLine("面积： {0}", GetArea());
>       }
>    }//end class Rectangle  
>    class Tabletop : Rectangle
>    {
>       private double cost;
>       public Tabletop(double l, double w) : base(l, w)
>       { }
>       public double GetCost()
>       {
>          double cost;
>          cost = GetArea() * 70;
>          return cost;
>       }
>       public void Display()
>       {
>          base.Display();
>          Console.WriteLine("成本： {0}", GetCost());
>       }
>    }
>    class ExecuteRectangle
>    {
>       static void Main(string[] args)
>       {
>          Tabletop t = new Tabletop(4.5, 7.5);
>          t.Display();
>          Console.ReadLine();
>       }
>    }
> }
> ```

#### 多重继承

> 多重继承指的是一个类别可以同时从多于一个父类继承行为与特征的功能
>
> 与单一继承相对，单一继承指一个类别只可以继承自一个父类
>
> **C# 不支持多重继承** , 但是，可以使用接口来实现多重继承

### 多态性

> 多态是同一个行为具有多个不同表现形式或形态的能力
>
> **多态性**意味着有多重形式。在面向对象编程范式中，多态性往往表现为"一个接口，多个功能"。
>
> 多态性可以是静态的或动态的。在**静态多态性**中，函数的响应是在编译时发生的。在**动态多态性**中，函数的响应是在运行时发生的。
>
> 在 C# 中，每个类型都是多态的，因为包括用户定义类型在内的所有类型都继承自 Object。

- 多态就是同一个接口，使用不同的实例而执行不同操作，如图所示：

![image-20230312150123631](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303121501697.png)

> 现实中，比如我们按下 F1 键这个动作：
>
> - 如果当前在 Flash 界面下弹出的就是 AS 3 的帮助文档；
> - 如果当前在 Word 下弹出的就是 Word 帮助；
> - 在 Windows 下弹出的就是 Windows 帮助和支持。

#### 静态多态性

> 在编译时，函数和对象的连接机制被称为早期绑定，也被称为静态绑定
>
> C# 提供了两种技术来实现静态多态性。分别为：
>
> - 函数重载
> - 运算符重载

#### 函数重载

> 您可以在同一个范围内对相同的函数名有多个定义
>
> 函数的定义必须彼此不同，可以是参数列表中的参数类型不同，也可以是参数个数不同
>
> 不能重载只有返回类型不同的函数声明

#### 动态多态性(难点)

> 一句话说明白：抽象类的派生类，必须重写抽象方法，virtual和abstract都修饰父类

- 抽象方法

> C# 允许使用关键字 **abstract** 创建抽象类，用于提供接口的部分类的实现。当一个派生类继承自该抽象类时，实现即完成。**抽象类**包含抽象方法，抽象方法可被派生类实现。
>
> 请注意，下面是有关抽象类的一些规则：
>
> - 不能创建一个抽象类的实例。
> - 不能在一个抽象类外部声明一个抽象方法。
> - 通过在类定义前面放置关键字 **sealed**，可以将类声明为**密封类**。当一个类被声明为 **sealed** 时，它不能被继承。抽象类不能被声明为 sealed。
>
> ```C#
> //抽象类实例
> using System;
> namespace PolymorphismApplication
> {
>    abstract class Shape
>    {
>        abstract public int area();
>    }
>    class Rectangle:  Shape
>    {
>       private int length;
>       private int width;
>       public Rectangle( int a=0, int b=0)
>       {
>          length = a;
>          width = b;
>       }
>       public override int area ()
>       {
>          Console.WriteLine("Rectangle 类的面积：");
>          return (width * length);
>       }
>    }
> 
>    class RectangleTester
>    {
>       static void Main(string[] args)
>       {
>          Rectangle r = new Rectangle(10, 7);
>          double a = r.area();
>          Console.WriteLine("面积： {0}",a);
>          Console.ReadKey();
>       }
>    }
> }
> ```



- 虚方法

> 当有一个定义在类中的函数需要在继承类中实现时，可以使用**虚方法**。
>
> 虚方法是使用关键字 **virtual** 声明的。
>
> 虚方法可以在不同的继承类中有不同的实现。
>
> 对虚方法的调用是在运行时发生的。
>
> 动态多态性是通过 **抽象类** 和 **虚方法** 实现的。

 

> 实例创建了 Shape 基类，并创建派生类 Circle、 Rectangle、Triangle
>
>  Shape 类提供一个名为 Draw 的虚拟方法，在每个派生类中重写该方法以绘制该类的指定形状
>
> ```C#
> using System;
> using System.Collections.Generic;
> 
> public class Shape
> {
>     public int X { get; private set; }
>     public int Y { get; private set; }
>     public int Height { get; set; }
>     public int Width { get; set; }
>    
>     // 虚方法
>     public virtual void Draw()
>     {
>         Console.WriteLine("执行基类的画图任务");
>     }
> }
> 
> class Circle : Shape
> {
>     public override void Draw()
>     {
>         Console.WriteLine("画一个圆形");
>         base.Draw();
>     }
> }
> class Rectangle : Shape
> {
>     public override void Draw()
>     {
>         Console.WriteLine("画一个长方形");
>         base.Draw();
>     }
> }
> class Triangle : Shape
> {
>     public override void Draw()
>     {
>         Console.WriteLine("画一个三角形");
>         base.Draw();
>     }
> }
> 
> class Program
> {
>     static void Main(string[] args)
>     {
>         // 创建一个 List<Shape> 对象，并向该对象添加 Circle、Triangle 和 Rectangle
>         var shapes = new List<Shape>
>         {
>             new Rectangle(),
>             new Triangle(),
>             new Circle()
>         };
> 
>         // 使用 foreach 循环对该列表的派生类进行循环访问，并对其中的每个 Shape 对象调用 Draw 方法
>         foreach (var shape in shapes)
>         {
>             shape.Draw();
>         }
> 
>         Console.WriteLine("按下任意键退出。");
>         Console.ReadKey();
>     }
> 
> }
> ```
>
> 通过虚方法 area() 来计算不同形状图像的面积：
>
> ```C#
> using System;
> namespace PolymorphismApplication
> {
>    class Shape
>    {
>       protected int width, height;
>       public Shape( int a=0, int b=0)
>       {
>          width = a;
>          height = b;
>       }
>       public virtual int area()
>       {
>          Console.WriteLine("父类的面积：");
>          return 0;
>       }
>    }
>    class Rectangle: Shape
>    {
>       public Rectangle( int a=0, int b=0): base(a, b)
>       {
> 
>       }
>       public override int area ()
>       {
>          Console.WriteLine("Rectangle 类的面积：");
>          return (width * height);
>       }
>    }
>    class Triangle: Shape
>    {
>       public Triangle(int a = 0, int b = 0): base(a, b)
>       {
>      
>       }
>       public override int area()
>       {
>          Console.WriteLine("Triangle 类的面积：");
>          return (width * height / 2);
>       }
>    }
>    class Caller
>    {
>       public void CallArea(Shape sh)
>       {
>          int a;
>          a = sh.area();
>          Console.WriteLine("面积： {0}", a);
>       }
>    }  
>    class Tester
>    {
>      
>       static void Main(string[] args)
>       {
>          Caller c = new Caller();
>          Rectangle r = new Rectangle(10, 7);
>          Triangle t = new Triangle(10, 5);
>          c.CallArea(r);	
>          c.CallArea(t);
>          Console.ReadKey();
>       }
>    }
> }
> ```

#### virtual 和 abstract

> virtual和abstract都是用来修饰父类的，通过覆盖父类的定义，让子类重新定义。
>
> -  1.virtual修饰的方法必须有实现（哪怕是仅仅添加一对大括号),而abstract修饰的方法一定不能实现。
> -  2.virtual可以被子类重写，而abstract必须被子类重写。
> -  3.如果类成员被abstract修饰，则该类前必须添加abstract，因为只有抽象类才可以有抽象方法。
> -  4.无法创建abstract类的实例，只能被继承无法实例化。

#### 重载和重写

> 重载(overload)是提供了一种机制, 相同函数名通过不同的返回值类型以及参数来表来区分的机制。
>
> 重写(override)是用于重写基类的虚方法,这样在派生类中提供一个新的方法。

#### 隐藏方法

> 在派生类中定义的和基类中的某个方法同名的方法，使用 new 关键字定义
>
> 如在基类 Animal 中有一方法 Sleep():
>
> ```C#
> public void Sleep()
> {
>     Console.WriteLine("Animal Sleep");
> }
> ```
>
> 则在派生类 Cat 中定义隐藏方法的代码为：
>
> ```C#
> new public void Sleep()
> {
>     Console.WriteLine("Cat Sleep");
> }
> ```
>
> 或者为：
>
> ```C#
> public new void Sleep()
> {
>     Console.WriteLine("Cat Sleep");
> } 
> ```

> - （1）隐藏方法不但可以隐藏基类中的虚方法，而且也可以隐藏基类中的非虚方法。
> - （2）隐藏方法中父类的实例调用父类的方法，子类的实例调用子类的方法。
> - （3）重写方法中子类的变量调用子类重写的方法，父类的变量要看这个父类引用的是子类的实例还是本身的实例，如果引用的是父类的实例那么调用基类的方法，如果引用的是派生类的实例则调用派生类的方法

### C# 运算符重载

> 重载运算符是具有特殊名称的函数，是通过关键字 **operator** 后跟运算符的符号来定义的
>
> 与其他函数一样，重载运算符有返回类型和参数列表

- 实例

```C#
using System;

namespace OperatorOvlApplication
{
   class Box
   {
      private double length;      // 长度
      private double breadth;     // 宽度
      private double height;      // 高度

      public double getVolume()
      {
         return length * breadth * height;
      }
      public void setLength( double len )
      {
         length = len;
      }

      public void setBreadth( double bre )
      {
         breadth = bre;
      }

      public void setHeight( double hei )
      {
         height = hei;
      }
      // 重载 + 运算符来把两个 Box 对象相加
      public static Box operator+ (Box b, Box c)
      {
         Box box = new Box();
         box.length = b.length + c.length;
         box.breadth = b.breadth + c.breadth;
         box.height = b.height + c.height;
         return box;
      }

   }

   class Tester
   {
      static void Main(string[] args)
      {
         Box Box1 = new Box();         // 声明 Box1，类型为 Box
         Box Box2 = new Box();         // 声明 Box2，类型为 Box
         Box Box3 = new Box();         // 声明 Box3，类型为 Box
         double volume = 0.0;          // 体积

         // Box1 详述
         Box1.setLength(6.0);
         Box1.setBreadth(7.0);
         Box1.setHeight(5.0);

         // Box2 详述
         Box2.setLength(12.0);
         Box2.setBreadth(13.0);
         Box2.setHeight(10.0);

         // Box1 的体积
         volume = Box1.getVolume();
         Console.WriteLine("Box1 的体积： {0}", volume);

         // Box2 的体积
         volume = Box2.getVolume();
         Console.WriteLine("Box2 的体积： {0}", volume);

         // 把两个对象相加
         Box3 = Box1 + Box2;

         // Box3 的体积
         volume = Box3.getVolume();
         Console.WriteLine("Box3 的体积： {0}", volume);
         Console.ReadKey();
      }
   }
}
```

#### 可重载和不可重载运算符

| 运算符                                | 描述                                         |
| :------------------------------------ | :------------------------------------------- |
| +, -, !, ~, ++, --                    | 这些一元运算符只有一个操作数，且可以被重载。 |
| +, -, *, /, %                         | 这些二元运算符带有两个操作数，且可以被重载。 |
| ==, !=, <, >, <=, >=                  | 这些比较运算符可以被重载。                   |
| &&, \|\|                              | 这些条件逻辑运算符不能被直接重载。           |
| +=, -=, *=, /=, %=                    | 这些赋值运算符不能被重载。                   |
| =, ., ?:, ->, new, is, sizeof, typeof | 这些运算符不能被重载。                       |

- 实例

```C#
using System;

namespace OperatorOvlApplication
{
    class Box
    {
       private double length;      // 长度
       private double breadth;     // 宽度
       private double height;      // 高度
     
       public double getVolume()
       {
         return length * breadth * height;
       }
      public void setLength( double len )
      {
          length = len;
      }

      public void setBreadth( double bre )
      {
          breadth = bre;
      }

      public void setHeight( double hei )
      {
          height = hei;
      }
      // 重载 + 运算符来把两个 Box 对象相加
      public static Box operator+ (Box b, Box c)
      {
          Box box = new Box();
          box.length = b.length + c.length;
          box.breadth = b.breadth + c.breadth;
          box.height = b.height + c.height;
          return box;
      }
     
      public static bool operator == (Box lhs, Box rhs)
      {
          bool status = false;
          if (lhs.length == rhs.length && lhs.height == rhs.height
             && lhs.breadth == rhs.breadth)
          {
              status = true;
          }
          return status;
      }
      public static bool operator !=(Box lhs, Box rhs)
      {
          bool status = false;
          if (lhs.length != rhs.length || lhs.height != rhs.height
              || lhs.breadth != rhs.breadth)
          {
              status = true;
          }
          return status;
      }
      public static bool operator <(Box lhs, Box rhs)
      {
          bool status = false;
          if (lhs.length < rhs.length && lhs.height
              < rhs.height && lhs.breadth < rhs.breadth)
          {
              status = true;
          }
          return status;
      }

      public static bool operator >(Box lhs, Box rhs)
      {
          bool status = false;
          if (lhs.length > rhs.length && lhs.height
              > rhs.height && lhs.breadth > rhs.breadth)
          {
              status = true;
          }
          return status;
      }

      public static bool operator <=(Box lhs, Box rhs)
      {
          bool status = false;
          if (lhs.length <= rhs.length && lhs.height
              <= rhs.height && lhs.breadth <= rhs.breadth)
          {
              status = true;
          }
          return status;
      }

      public static bool operator >=(Box lhs, Box rhs)
      {
          bool status = false;
          if (lhs.length >= rhs.length && lhs.height
             >= rhs.height && lhs.breadth >= rhs.breadth)
          {
              status = true;
          }
          return status;
      }
      public override string ToString()
      {
          return String.Format("({0}, {1}, {2})", length, breadth, height);
      }
   
   }
   
   class Tester
   {
      static void Main(string[] args)
      {
        Box Box1 = new Box();          // 声明 Box1，类型为 Box
        Box Box2 = new Box();          // 声明 Box2，类型为 Box
        Box Box3 = new Box();          // 声明 Box3，类型为 Box
        Box Box4 = new Box();
        double volume = 0.0;   // 体积

        // Box1 详述
        Box1.setLength(6.0);
        Box1.setBreadth(7.0);
        Box1.setHeight(5.0);

        // Box2 详述
        Box2.setLength(12.0);
        Box2.setBreadth(13.0);
        Box2.setHeight(10.0);

       // 使用重载的 ToString() 显示两个盒子
        Console.WriteLine("Box1： {0}", Box1.ToString());
        Console.WriteLine("Box2： {0}", Box2.ToString());
       
        // Box1 的体积
        volume = Box1.getVolume();
        Console.WriteLine("Box1 的体积： {0}", volume);

        // Box2 的体积
        volume = Box2.getVolume();
        Console.WriteLine("Box2 的体积： {0}", volume);

        // 把两个对象相加
        Box3 = Box1 + Box2;
        Console.WriteLine("Box3： {0}", Box3.ToString());
        // Box3 的体积
        volume = Box3.getVolume();
        Console.WriteLine("Box3 的体积： {0}", volume);

        //comparing the boxes
        if (Box1 > Box2)
          Console.WriteLine("Box1 大于 Box2");
        else
          Console.WriteLine("Box1 不大于 Box2");
        if (Box1 < Box2)
          Console.WriteLine("Box1 小于 Box2");
        else
          Console.WriteLine("Box1 不小于 Box2");
        if (Box1 >= Box2)
          Console.WriteLine("Box1 大于等于 Box2");
        else
          Console.WriteLine("Box1 不大于等于 Box2");
        if (Box1 <= Box2)
          Console.WriteLine("Box1 小于等于 Box2");
        else
          Console.WriteLine("Box1 不小于等于 Box2");
        if (Box1 != Box2)
          Console.WriteLine("Box1 不等于 Box2");
        else
          Console.WriteLine("Box1 等于 Box2");
        Box4 = Box3;
        if (Box3 == Box4)
          Console.WriteLine("Box3 等于 Box4");
        else
          Console.WriteLine("Box3 不等于 Box4");

        Console.ReadKey();
      }
    }
}
```

#### 一些细节

> operator 关键字用于在类或结构声明中声明运算符。运算符声明可以采用下列四种形式之一：
>
> ```C#
> public static result-type operator unary-operator ( op-type operand )
> public static result-type operator binary-operator ( op-type operand, op-type2 operand2 )
> public static implicit operator conv-type-out ( conv-type-in operand )
> public static explicit operator conv-type-out ( conv-type-in operand )
> ```
>
> 参数：
>
> -  result-type 运算符的结果类型。
> -  unary-operator 下列运算符之一：+ - ! ~ ++ — true false
> -  op-type 第一个（或唯一一个）参数的类型。
> -  operand 第一个（或唯一一个）参数的名称。
> -  binary-operator 其中一个：+ - * / % & | ^ << >> == != > < >= <=
> -  op-type2 第二个参数的类型。
> -  operand2 第二个参数的名称。
> -  conv-type-out 类型转换运算符的目标类型。
> -  conv-type-in 类型转换运算符的输入类型。

> 注意：
>
> 前两种形式声明了用户定义的重载内置运算符的运算符。并非所有内置运算符都可以被重载。op-type 和 op-type2 中至少有一个必须是封闭类型（即运算符所属的类型，或理解为自定义的类型）。例如，这将防止重定义整数加法运算符。
>
> 后两种形式声明了转换运算符。conv-type-in 和 conv-type-out 中正好有一个必须是封闭类型（即，转换运算符只能从它的封闭类型转换为其他某个类型，或从其他某个类型转换为它的封闭类型）。
>
> 运算符只能采用值参数，不能采用 ref 或 out 参数。
>
> C# 要求成对重载比较运算符。如果重载了==，则也必须重载!=，否则产生编译错误。同时，比较运算符必须返回bool类型的值，这是与其他算术运算符的根本区别。
>
> C# 不允许重载=运算符，但如果重载例如+运算符，编译器会自动使用+运算符的重载来执行+=运算符的操作。
>
> 运算符重载的其实就是函数重载。首先通过指定的运算表达式调用对应的运算符函数，然后再将运算对象转化为运算符函数的实参，接着根据实参的类型来确定需要调用的函数的重载，这个过程是由编译器完成。
>
> 任何运算符声明的前面都可以有一个可选的属性列表

### 接口

> 接口定义了所有类继承接口时应遵循的语法合同。接口定义了语法合同 **"是什么"** 部分，派生类定义了语法合同 **"怎么做"** 部分。
>
> 接口定义了属性、方法和事件，这些都是接口的成员。接口只包含了成员的声明。成员的定义是派生类的责任。接口提供了派生类应遵循的标准结构。
>
> 接口使得实现接口的类或结构在形式上保持一致。
>
> 抽象类在某种程度上与接口类似，但是，它们大多只是用在当只有少数方法由基类声明由派生类实现时。
>
> 接口本身并不实现任何功能，它只是和声明实现该接口的对象订立一个必须实现哪些行为的契约。
>
> 抽象类不能直接实例化，但允许派生出具体的，具有实际功能的类。

#### 定义接口：MyInterface.cs

> 接口使用 **interface** 关键字声明，它与类的声明类似。接口声明默认是 public 的。
>
> 下面是一个接口声明的实例：
>
> ```C#
> interface IMyInterface
> {
>   void MethodToImplement();
> }
> ```
>
> 以上代码定义了接口 IMyInterface。通常接口命令以 **I** 字母开头，这个接口只有一个方法 MethodToImplement()，没有参数和返回值，当然我们可以按照需求设置参数和返回值。
>
> 值得注意的是，该方法并没有具体的实现。
>
>  
>
> 如何实现接口？
>
> ```C#
> using System;
> 
> interface IMyInterface
> {
>         // 接口成员
>     void MethodToImplement();
> }
> 
> class InterfaceImplementer : IMyInterface
> {
>     static void Main()
>     {
>         InterfaceImplementer iImp = new InterfaceImplementer();
>         iImp.MethodToImplement();
>     }
> 
>     public void MethodToImplement()
>     {
>         Console.WriteLine("MethodToImplement() called.");
>     }
> }
> ```
>
> InterfaceImplementer 类实现了 IMyInterface 接口，接口的实现与类的继承语法格式类似

#### 接口继承: InterfaceInheritance.cs

> 以下实例定义了两个接口 IMyInterface 和 IParentInterface
>
> 如果一个接口继承其他接口，那么实现类或结构就需要实现所有接口的成员
>
> ```C#
> using System;
> 
> interface IParentInterface
> {
>     void ParentInterfaceMethod();
> }
> 
> interface IMyInterface : IParentInterface
> {
>     void MethodToImplement();
> }
> 
> class InterfaceImplementer : IMyInterface
> {
>     static void Main()
>     {
>         InterfaceImplementer iImp = new InterfaceImplementer();
>         iImp.MethodToImplement();
>         iImp.ParentInterfaceMethod();
>     }
> 
>     public void MethodToImplement()
>     {
>         Console.WriteLine("MethodToImplement() called.");
>     }
> 
>     public void ParentInterfaceMethod()
>     {
>         Console.WriteLine("ParentInterfaceMethod() called.");
>     }
> }
> ```

### 命名空间（Namespace）

> **命名空间**的设计目的是提供一种让一组名称与其他名称分隔开的方式
>
> 在一个命名空间中声明的类的名称与另一个命名空间中声明的相同的类的名称不冲突
>
> 我们举一个计算机系统中的例子，一个文件夹(目录)中可以包含多个文件夹，每个文件夹中不能有相同的文件名，但不同文件夹中的文件可以重名。

![image-20230312164623611](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303121646667.png)

#### 定义命名空间

> 命名空间的定义是以关键字 **namespace** 开始，后跟命名空间的名称
>
> ```C#
> namespace namespace_name
> {
>    // 代码声明
> }
> ```

#### using关键字

> **using** 关键字表明程序使用的是给定命名空间中的名称。例如，我们在程序中使用 **System** 命名空间，其中定义了类 Console。我们可以只写：
>
> ```C#
> Console.WriteLine ("Hello there");
> ```
>
> 我们可以写完全限定名称，如下：
>
> ```C#
> System.Console.WriteLine("Hello there");
> ```

##### using用法

**1. using指令：引入命名空间**

这是最常见的用法，例如：

```C#
using System;
using Namespace1.SubNameSpace;
```

**2. using static 指令：指定无需指定类型名称即可访问其静态成员的类型**

```C#
using static System.Math;var = PI; // 直接使用System.Math.PI
```

**3. 起别名**

```C#
using Project = PC.MyCompany.Project;
```

**4. using语句：将实例与代码绑定**

```C#
using (Font font3 = new Font("Arial", 10.0f),
            font4 = new Font("Arial", 10.0f))
{
    // Use font3 and font4.
}
```

代码段结束时，自动调用font3和font4的Dispose方法，释放实例

#### 嵌套命名空间

> 命名空间可以被嵌套，即可以在一个命名空间内定义另一个命名空间
>
> ```C#
> namespace namespace_name1 
> {
>    // 代码声明
>    namespace namespace_name2 
>    {
>      // 代码声明
>    }
> }
> ```

> 您可以使用点（.）运算符访问嵌套的命名空间的成员，如下所示：
>
> ```C#
> using System;
> using SomeNameSpace;
> using SomeNameSpace.Nested;
> 
> namespace SomeNameSpace
> {
>     public class MyClass
>     {
>         static void Main()
>         {
>             Console.WriteLine("In SomeNameSpace");
>             Nested.NestedNameSpaceClass.SayHello();		//访问内嵌命名空间的函数
>         }
>     }
> 
>     // 内嵌命名空间
>     namespace Nested  
>     {
>         public class NestedNameSpaceClass
>         {
>             public static void SayHello()
>             {
>                 Console.WriteLine("In Nested");
>             }
>         }
>     }
> }
> ```

### 预处理指令

> 预处理器指令指导编译器在实际编译开始之前对信息进行预处理
>
> 所有的预处理器指令都是以 # 开始。且在一行上，只有空白字符可以出现在预处理器指令之前，预处理器指令不是语句，所以它们不以分号（;）结束

> C# 编译器没有一个单独的预处理器，但是，指令被处理时就像是有一个单独的预处理器一样
>
> 在 C# 中，预处理器指令用于在条件编译中起作用
>
> 与 C 和 C++ 不同的是，它们不是用来创建宏
>
> 一个预处理器指令必须是该行上的唯一指令

- 预处理指令

| 预处理器指令 | 描述                                                         |
| :----------- | :----------------------------------------------------------- |
| #define      | 它用于定义一系列成为符号的字符。                             |
| #undef       | 它用于取消定义符号。                                         |
| #if          | 它用于测试符号是否为真。                                     |
| #else        | 它用于创建复合条件指令，与 #if 一起使用。                    |
| #elif        | 它用于创建复合条件指令。                                     |
| #endif       | 指定一个条件指令的结束。                                     |
| #line        | 它可以让您修改编译器的行数以及（可选地）输出错误和警告的文件名。 |
| #error       | 它允许从代码的指定位置生成一个错误。                         |
| #warning     | 它允许从代码的指定位置生成一级警告。                         |
| #region      | 它可以让您在使用 Visual Studio Code Editor 的大纲特性时，指定一个可展开或折叠的代码块。 |
| #endregion   | 它标识着 #region 块的结束。                                  |

#### #define 预处理器

> \#define 预处理器指令创建符号常量
>
> 可以禁止编译器编译 某一部分代码

> 语法如下：
>
> ```C#
> #define symbol
> ```
>
> ```C#
> #define PI
> using System;
> namespace PreprocessorDAppl
> {
>    class Program
>    {
>       static void Main(string[] args)
>       {
>          #if (PI)
>             Console.WriteLine("PI is defined");
>          #else
>             Console.WriteLine("PI is not defined");
>          #endif
>          Console.ReadKey();
>       }
>    }
> }
> ```
>
> ```
> PI is defined
> ```

### 正则表达式

> **正则表达式** 是一种匹配输入文本的模式。
>
> .Net 框架提供了允许这种匹配的正则表达式引擎。

#### 转义字符

| 转义字符      | 描述                                                         | 模式                        | 匹配                                     |
| :------------ | :----------------------------------------------------------- | :-------------------------- | :--------------------------------------- |
| **\a**        | 与报警 (bell) 符 \u0007 匹配。                               | \a                          | "Warning!" + '\u0007' 中的 "\u0007"      |
| **\b**        | 在字符类中，与退格键 \u0008 匹配。                           | [\b]{3,}                    | "\b\b\b\b" 中的 "\b\b\b\b"               |
| **\t**        | 与制表符 \u0009 匹配。                                       | (\w+)\t                     | "Name\tAddr\t" 中的 "Name\t" 和 "Addr\t" |
| **\r**        | 与回车符 \u000D 匹配。（\r 与换行符 \n 不是等效的。）        | \r\n(\w+)                   | "\r\nHello\nWorld." 中的 "\r\nHello"     |
| **\v**        | 与垂直制表符 \u000B 匹配。                                   | [\v]{2,}                    | "\v\v\v" 中的 "\v\v\v"                   |
| **\f**        | 与换页符 \u000C 匹配。                                       | [\f]{2,}                    | "\f\f\f" 中的 "\f\f\f"                   |
| **\n**        | 与换行符 \u000A 匹配。                                       | \r\n(\w+)                   | "\r\nHello\nWorld." 中的 "\r\nHello"     |
| **\e**        | 与转义符 \u001B 匹配。                                       | \e                          | "\x001B" 中的 "\x001B"                   |
| **\ nnn**     | 使用八进制表示形式指定一个字符（nnn 由二到三位数字组成）。   | \w\040\w                    | "a bc d" 中的 "a b" 和 "c d"             |
| **\x nn**     | 使用十六进制表示形式指定字符（nn 恰好由两位数字组成）。      | \w\x20\w                    | "a bc d" 中的 "a b" 和 "c d"             |
| **\c X \c x** | 匹配 X 或 x 指定的 ASCII 控件字符，其中 X 或 x 是控件字符的字母。 | \cC                         | "\x0003" 中的 "\x0003" (Ctrl-C)          |
| **\u nnnn**   | 使用十六进制表示形式匹配一个 Unicode 字符（由 nnnn 表示的四位数）。 | \w\u0020\w                  | "a bc d" 中的 "a b" 和 "c d"             |
| **\\**        | 在后面带有不识别的转义字符时，与该字符匹配。                 | \d+[\+-x\*]\d+\d+[\+-x\*\d+ | "(2+2) * 3*9" 中的 "2+2" 和 "3*9"        |

#### 字符类

> **字符类与一组字符中的任何一个字符匹配**

| 字符类                 | 描述                                                         | 模式   | 匹配                                       |
| :--------------------- | :----------------------------------------------------------- | :----- | :----------------------------------------- |
| **[character_group]**  | 匹配 character_group 中的任何单个字符。 默认情况下，匹配区分大小写。 | [mn]   | "mat" 中的 "m"，"moon" 中的 "m" 和 "n"     |
| **[^character_group]** | 非：与不在 character_group 中的任何单个字符匹配。 默认情况下，character_group 中的字符区分大小写。 | [^aei] | "avail" 中的 "v" 和 "l"                    |
| **[ first - last ]**   | 字符范围：与从 first 到 last 的范围中的任何单个字符匹配。    | [b-d]  | [b-d]irds 可以匹配 Birds、 Cirds、 Dirds   |
| **.**                  | 通配符：与除 \n 之外的任何单个字符匹配。 若要匹配原意句点字符（. 或 \u002E），您必须在该字符前面加上转义符 (\.)。 | a.e    | "have" 中的 "ave"， "mate" 中的 "ate"      |
| **\p{ name }**         | 与 *name* 指定的 Unicode 通用类别或命名块中的任何单个字符匹配。 | \p{Lu} | "City Lights" 中的 "C" 和 "L"              |
| **\P{ name }**         | 与不在 *name* 指定的 Unicode 通用类别或命名块中的任何单个字符匹配。 | \P{Lu} | "City" 中的 "i"、 "t" 和 "y"               |
| **\w**                 | 与任何单词字符匹配。                                         | \w     | "Room#1" 中的 "R"、 "o"、 "m" 和 "1"       |
| **\W**                 | 与任何非单词字符匹配。                                       | \W     | "Room#1" 中的 "#"                          |
| **\s**                 | 与任何空白字符匹配。                                         | \w\s   | "ID A1.3" 中的 "D "                        |
| **\S**                 | 与任何非空白字符匹配。                                       | \s\S   | "int __ctr" 中的 " _"                      |
| **\d**                 | 与任何十进制数字匹配。                                       | \d     | "4 = IV" 中的 "4"                          |
| **\D**                 | 匹配不是十进制数的任意字符。                                 | \D     | "4 = IV" 中的 " "、 "="、 " "、 "I" 和 "V" |

#### 定位点

> 定位点或原子零宽度断言会使匹配成功或失败，具体取决于字符串中的当前位置，但它们不会使引擎在字符串中前进或使用字符

| 断言   | 描述                                                         | 模式     | 匹配                                            |
| :----- | :----------------------------------------------------------- | :------- | :---------------------------------------------- |
| **^**  | 匹配必须从字符串或一行的开头开始。                           | ^\d{3}   | "567-777-" 中的 "567"                           |
| **$**  | 匹配必须出现在字符串的末尾或出现在行或字符串末尾的 **\n** 之前。 | -\d{4}$  | "8-12-2012" 中的 "-2012"                        |
| **\A** | 匹配必须出现在字符串的开头。                                 | \A\w{4}  | "Code-007-" 中的 "Code"                         |
| **\Z** | 匹配必须出现在字符串的末尾或出现在字符串末尾的 **\n** 之前。 | -\d{3}\Z | "Bond-901-007" 中的 "-007"                      |
| **\z** | 匹配必须出现在字符串的末尾。                                 | -\d{3}\z | "-901-333" 中的 "-333"                          |
| **\G** | 匹配必须出现在上一个匹配结束的地方。                         | \G\(\d\) | "(1)(3)(5)[7](9)" 中的 "(1)"、 "(3)" 和 "(5)"   |
| **\b** | 匹配一个单词边界，也就是指单词和空格间的位置。               | er\b     | 匹配"never"中的"er"，但不能匹配"verb"中的"er"。 |
| **\B** | 匹配非单词边界。                                             | er\B     | 匹配"verb"中的"er"，但不能匹配"never"中的"er"。 |

#### 分组构造

> 分组构造描述了正则表达式的子表达式，通常用于捕获输入字符串的子字符串

| 分组构造                             | 描述                                                 | 模式                                                         | 匹配                                                         |
| :----------------------------------- | :--------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **( subexpression )**                | 捕获匹配的子表达式并将其分配到一个从零开始的序号中。 | (\w)\1                                                       | "deep" 中的 "ee"                                             |
| **(?< name >subexpression)**         | 将匹配的子表达式捕获到一个命名组中。                 | (?< double>\w)\k< double>                                    | "deep" 中的 "ee"                                             |
| **(?< name1 -name2 >subexpression)** | 定义平衡组定义。                                     | (((?'Open'\()\[\^\(\)]*)+((?'Close-Open'\))\[\^\(\)]*)+)*(?(Open)(?!))$ | "3+2^((1-3)*(3-1))" 中的 "((1-3)*(3-1))"                     |
| **(?: subexpression)**               | 定义非捕获组。                                       | Write(?:Line)?                                               | "Console.WriteLine()" 中的 "WriteLine"                       |
| **(?imnsx-imnsx:subexpression)**     | 应用或禁用 *subexpression* 中指定的选项。            | A\d{2}(?i:\w+)\b                                             | "A12xl A12XL a12xl" 中的 "A12xl" 和 "A12XL"                  |
| **(?= subexpression)**               | 零宽度正预测先行断言。                               | \w+(?=\.)                                                    | "He is. The dog ran. The sun is out." 中的 "is"、 "ran" 和 "out" |
| **(?! subexpression)**               | 零宽度负预测先行断言。                               | \b(?!un)\w+\b                                                | "unsure sure unity used" 中的 "sure" 和 "used"               |
| **(?<=subexpression)**               | 零宽度正回顾后发断言。                               | (?<=19)\d{2}\b                                               | "1851 1999 1950 1905 2003" 中的 "99"、"50"和 "05"            |
| **(?<! subexpression)**              | 零宽度负回顾后发断言。                               | (?<!wo)man\b                                                 | "Hi woman Hi man" 中的 "man"                                 |
| **(?> subexpression)**               | 非回溯（也称为"贪婪"）子表达式。                     | \[13579](?>A+B+)                                             | "1ABB 3ABBC 5AB 5AC" 中的 "1ABB"、 "3ABB" 和 "5AB"           |

#### 限定符

> 限定符指定在输入字符串中必须存在上一个元素（可以是字符、组或字符类）的多少个实例才能出现匹配项。 限定符包括下表中列出的语言元素。

| 限定符         | 描述                                                   | 模式       | 匹配                                                         |
| :------------- | :----------------------------------------------------- | :--------- | :----------------------------------------------------------- |
| *****          | 匹配上一个元素零次或多次。                             | \d*\.\d    | ".0"、 "19.9"、 "219.9"                                      |
| **+**          | 匹配上一个元素一次或多次。                             | "be+"      | "been" 中的 "bee"， "bent" 中的 "be"                         |
| **?**          | 匹配上一个元素零次或一次。                             | "rai?n"    | "ran"、 "rain"                                               |
| **{ n }**      | 匹配上一个元素恰好 n 次。                              | ",\d{3}"   | "1,043.6" 中的 ",043"， "9,876,543,210" 中的 ",876"、 ",543" 和 ",210" |
| **{ n ,}**     | 匹配上一个元素至少 n 次。                              | "\d{2,}"   | "166"、 "29"、 "1930"                                        |
| **{ n , m }**  | 匹配上一个元素至少 n 次，但不多于 m 次。               | "\d{3,5}"  | "166"， "17668"， "193024" 中的 "19302"                      |
| ***?**         | 匹配上一个元素零次或多次，但次数尽可能少。             | \d*?\.\d   | ".0"、 "19.9"、 "219.9"                                      |
| **+?**         | 匹配上一个元素一次或多次，但次数尽可能少。             | "be+?"     | "been" 中的 "be"， "bent" 中的 "be"                          |
| **??**         | 匹配上一个元素零次或一次，但次数尽可能少。             | "rai??n"   | "ran"、 "rain"                                               |
| **{ n }?**     | 匹配前导元素恰好 n 次。                                | ",\d{3}?"  | "1,043.6" 中的 ",043"， "9,876,543,210" 中的 ",876"、 ",543" 和 ",210" |
| **{ n ,}?**    | 匹配上一个元素至少 n 次，但次数尽可能少。              | "\d{2,}?"  | "166"、 "29" 和 "1930"                                       |
| **{ n , m }?** | 匹配上一个元素的次数介于 n 和 m 之间，但次数尽可能少。 | "\d{3,5}?" | "166"， "17668"， "193024" 中的 "193" 和 "024"               |

#### 反向引用构造

> 反向引用允许在同一正则表达式中随后标识以前匹配的子表达式

| 反向引用构造   | 描述                                | 模式                  | 匹配             |
| :------------- | :---------------------------------- | :-------------------- | :--------------- |
| **\ number**   | 反向引用。 匹配编号子表达式的值。   | (\w)\1                | "seek" 中的 "ee" |
| **\k< name >** | 命名反向引用。 匹配命名表达式的值。 | (?< char>\w)\k< char> | "seek" 中的 "ee" |

#### 备用构造

> 备用构造用于修改正则表达式以启用 either/or 匹配

| 备用构造                        | 描述                                                         | 模式                                 | 匹配                                                         |
| :------------------------------ | :----------------------------------------------------------- | :----------------------------------- | :----------------------------------------------------------- |
| **\|**                          | 匹配以竖线 (\|) 字符分隔的任何一个元素。                     | th(e\|is\|at)                        | "this is the day. " 中的 "the" 和 "this"                     |
| **(?( expression )yes \| no )** | 如果正则表达式模式由 expression 匹配指定，则匹配 *yes*；否则匹配可选的 *no* 部分。 expression 被解释为零宽度断言。 | (?(A)A\d{2}\b\|\b\d{3}\b)            | "A10 C103 910" 中的 "A10" 和 "910"                           |
| **(?( name )yes \| no )**       | 如果 name 或已命名或已编号的捕获组具有匹配，则匹配 *yes*；否则匹配可选的 *no*。 | (?< quoted>")?(?(quoted).+?"\|\S+\s) | "Dogs.jpg "Yiska playing.jpg"" 中的 Dogs.jpg 和 "Yiska playing.jpg" |

#### 替换

> 替换是替换模式中使用的正则表达式

| 字符            | 描述                                 | 模式                                 | 替换模式          | 输入字符串 | 结果字符串   |
| :-------------- | :----------------------------------- | :----------------------------------- | :---------------- | :--------- | :----------- |
| **$**number     | 替换按组 *number* 匹配的子字符串。   | \b(\w+)(\s)(\w+)\b                   | $3$2$1            | "one two"  | "two one"    |
| **${**name**}** | 替换按命名组 *name* 匹配的子字符串。 | \b(?< word1>\w+)(\s)(?< word2>\w+)\b | ${word2} ${word1} | "one two"  | "two one"    |
| **$$**          | 替换字符"$"。                        | \b(\d+)\s?USD                        | $$$1              | "103 USD"  | "$103"       |
| **$&**          | 替换整个匹配项的一个副本。           | (\$*(\d*(\.+\d+)?){1})               | **$&              | "$1.30"    | "**$1.30"    |
| **$`**          | 替换匹配前的输入字符串的所有文本。   | B+                                   | $`                | "AABBCC"   | "AAAACC"     |
| **$'**          | 替换匹配后的输入字符串的所有文本。   | B+                                   | $'                | "AABBCC"   | "AACCCC"     |
| **$+**          | 替换最后捕获的组。                   | B+(C+)                               | $+                | "AABBCCDD" | AACCDD       |
| **$_**          | 替换整个输入字符串。                 | B+                                   | $_                | "AABBCC"   | "AAAABBCCCC" |

#### 杂项构造

| 构造               | 描述                                                   | 实例                                                   |
| :----------------- | :----------------------------------------------------- | :----------------------------------------------------- |
| **(?imnsx-imnsx)** | 在模式中间对诸如不区分大小写这样的选项进行设置或禁用。 | \bA(?i)b\w+\b 匹配 "ABA Able Act" 中的 "ABA" 和 "Able" |
| **(?#注释)**       | 内联注释。该注释在第一个右括号处终止。                 | \bA(?#匹配以A开头的单词)\w+\b                          |
| **#** [行尾]       | 该注释以非转义的 # 开头，并继续到行的结尾。            | (?x)\bA\w+\b#匹配以 A 开头的单词                       |

#### Regex 类

> Regex 类用于表示一个正则表达式

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public bool IsMatch( string input )** 指示 Regex 构造函数中指定的正则表达式是否在指定的输入字符串中找到匹配项。 |
| 2    | **public bool IsMatch( string input, int startat )** 指示 Regex 构造函数中指定的正则表达式是否在指定的输入字符串中找到匹配项，从字符串中指定的开始位置开始。 |
| 3    | **public static bool IsMatch( string input, string pattern )** 指示指定的正则表达式是否在指定的输入字符串中找到匹配项。 |
| 4    | **public MatchCollection Matches( string input )** 在指定的输入字符串中搜索正则表达式的所有匹配项。 |
| 5    | **public string Replace( string input, string replacement )** 在指定的输入字符串中，把所有匹配正则表达式模式的所有匹配的字符串替换为指定的替换字符串。 |
| 6    | **public string[] Split( string input )** 把输入字符串分割为子字符串数组，根据在 Regex 构造函数中指定的正则表达式模式定义的位置进行分割。 |

### 异常处理

> 异常是在程序执行期间出现的问题
>
> C# 中的异常是对程序运行时出现的特殊情况的一种响应，比如尝试除以零
>
> 异常提供了一种把程序控制权从某个部分转移到另一个部分的方式
>
> C# 异常处理时建立在四个关键词之上的：**try**、**catch**、**finally** 和 **throw**
>
> - **try**：一个 try 块标识了一个将被激活的特定的异常的代码块。后跟一个或多个 catch 块。
> - **catch**：程序通过异常处理程序捕获异常。catch 关键字表示异常的捕获。
> - **finally**：finally 块用于执行给定的语句，不管异常是否被抛出都会执行。例如，如果您打开一个文件，不管是否出现异常文件都要被关闭。
> - **throw**：当问题出现时，程序抛出一个异常。使用 throw 关键字来完成。

#### 语法

> 假设一个块将出现异常，一个方法使用 try 和 catch 关键字捕获异常
>
> 可以列出多个 catch 语句捕获不同类型的异常，以防 try 块在不同的情况下生成多个异常
>
> try/catch 块内的代码为受保护的代码，使用 try/catch 语法如下所示 : 
>
> ```C#
> try
> {
>    // 引起异常的语句
> }
> catch( ExceptionName e1 )
> {
>    // 错误处理代码
> }
> catch( ExceptionName e2 )
> {
>    // 错误处理代码
> }
> catch( ExceptionName eN )
> {
>    // 错误处理代码
> }
> finally
> {
>    // 要执行的语句
> }
> ```

#### C# 中的异常类

> C# 异常是使用类来表示的。C# 中的异常类主要是直接或间接地派生于 **System.Exception** 类**System.ApplicationException** 和 **System.SystemException** 类是派生于 System.Exception 类的异常类
>
> **System.ApplicationException** 类支持由应用程序生成的异常 , 所以程序员定义的异常都应派生自该类
>
> **System.SystemException** 类是所有预定义的系统异常的基类
>
> 下表列出了一些派生自 System.SystemException 类的预定义的异常类:

| 异常类                            | 描述                                           |
| :-------------------------------- | :--------------------------------------------- |
| System.IO.IOException             | 处理 I/O 错误。                                |
| System.IndexOutOfRangeException   | 处理当方法指向超出范围的数组索引时生成的错误。 |
| System.ArrayTypeMismatchException | 处理当数组类型不匹配时生成的错误。             |
| System.NullReferenceException     | 处理当依从一个空对象时生成的错误。             |
| System.DivideByZeroException      | 处理当除以零时生成的错误。                     |
| System.InvalidCastException       | 处理在类型转换期间生成的错误。                 |
| System.OutOfMemoryException       | 处理空闲内存不足生成的错误。                   |
| System.StackOverflowException     | 处理栈溢出生成的错误。                         |

#### 实例

```C#
using System;
namespace ErrorHandlingApplication
{
    class DivNumbers
    {
        int result;
        DivNumbers()
        {
            result = 0;
        }
        public void division(int num1, int num2)
        {
            try
            {
                result = num1 / num2;
            }
            catch (DivideByZeroException e)
            {
                Console.WriteLine("Exception caught: {0}", e);
            }
            finally
            {
                Console.WriteLine("Result: {0}", result);
            }

        }
        static void Main(string[] args)
        {
            DivNumbers d = new DivNumbers();
            d.division(25, 0);
            Console.ReadKey();
        }
    }
}
```

#### 创建用户自定义异常

> 可以定义自己的异常
>
> 用户自定义的异常类是派生自 **ApplicationException** 类

```C#
using System;
namespace UserDefinedException
{
   class TestTemperature
   {
      static void Main(string[] args)
      {
         Temperature temp = new Temperature();
         try
         {
            temp.showTemp();
         }
         catch(TempIsZeroException e)
         {
            Console.WriteLine("TempIsZeroException: {0}", e.Message);
         }
         Console.ReadKey();
      }
   }
}
public class TempIsZeroException: ApplicationException
{
   public TempIsZeroException(string message): base(message)
   {
   }
}
public class Temperature
{
   int temperature = 0;
   public void showTemp()
   {
      if(temperature == 0)
      {
         throw (new TempIsZeroException("Zero Temperature found"));
      }
      else
      {
         Console.WriteLine("Temperature: {0}", temperature);
      }
   }
}
```

#### 抛出对象

> 如果异常是直接或间接派生自 **System.Exception** 类，您可以抛出一个对象
>
> 可以在 catch 块中使用 throw 语句来抛出当前的对象

```c#
Catch(Exception e)
{
   ...
   Throw e
}
```

### 文件的输入与输出

> 一个 **文件** 是一个存储在磁盘中带有指定名称和目录路径的数据集合
>
> 当打开文件进行读写时，它变成一个 **流**
>
> 从根本上说，流是通过通信路径传递的字节序列
>
> **输入流**用于从文件读取数据（读操作），**输出流**用于向文件写入数据（写操作）

#### I/O 类

> System.IO 命名空间有各种不同的类，用于执行各种文件操作，如创建和删除文件、读取或写入文件，关闭文件等。
>
> 下表列出了一些 System.IO 命名空间中常用的非抽象类:

| I/O 类         | 描述                               |
| :------------- | :--------------------------------- |
| BinaryReader   | 从二进制流读取原始数据。           |
| BinaryWriter   | 以二进制格式写入原始数据。         |
| BufferedStream | 字节流的临时存储。                 |
| Directory      | 有助于操作目录结构。               |
| DirectoryInfo  | 用于对目录执行操作。               |
| DriveInfo      | 提供驱动器的信息。                 |
| File           | 有助于处理文件。                   |
| FileInfo       | 用于对文件执行操作。               |
| FileStream     | 用于文件中任何位置的读写。         |
| MemoryStream   | 用于随机访问存储在内存中的数据流。 |
| Path           | 对路径信息执行操作。               |
| StreamReader   | 用于从字节流中读取字符。           |
| StreamWriter   | 用于向一个流中写入字符。           |
| StringReader   | 用于读取字符串缓冲区。             |
| StringWriter   | 用于写入字符串缓冲区。             |

#### FileStream 类

> System.IO 命名空间中的 **FileStream** 类有助于文件的读写与关闭。该类派生自抽象类 Stream。
>
> 您需要创建一个 **FileStream** 对象来创建一个新的文件，或打开一个已有的文件
>
> 创建 **FileStream** 对象的语法如下:
>
> ```C#
> FileStream <object_name> = new FileStream( <file_name>,
> <FileMode Enumerator>, <FileAccess Enumerator>, <FileShare Enumerator>);
> ```

> 实例：
>
> ```C#
> FileStream F = new FileStream("sample.txt", FileMode.Open, FileAccess.Read, FileShare.Read);

| 参数       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| FileMode   | **FileMode** 枚举定义了各种打开文件的方法。FileMode 枚举的成员有：**Append**：打开一个已有的文件，并将光标放置在文件的末尾。如果文件不存在，则创建文件。**Create**：创建一个新的文件。如果文件已存在，则删除旧文件，然后创建新文件。**CreateNew**：指定操作系统应创建一个新的文件。如果文件已存在，则抛出异常。**Open**：打开一个已有的文件。如果文件不存在，则抛出异常。**OpenOrCreate**：指定操作系统应打开一个已有的文件。如果文件不存在，则用指定的名称创建一个新的文件打开。**Truncate**：打开一个已有的文件，文件一旦打开，就将被截断为零字节大小。然后我们可以向文件写入全新的数据，但是保留文件的初始创建日期。如果文件不存在，则抛出异常。 |
| FileAccess | **FileAccess** 枚举的成员有：**Read**、**ReadWrite** 和 **Write**。 |
| FileShare  | **FileShare** 枚举的成员有：**Inheritable**：允许文件句柄可由子进程继承。Win32 不直接支持此功能。**None**：谢绝共享当前文件。文件关闭前，打开该文件的任何请求（由此进程或另一进程发出的请求）都将失败。**Read**：允许随后打开文件读取。如果未指定此标志，则文件关闭前，任何打开该文件以进行读取的请求（由此进程或另一进程发出的请求）都将失败。但是，即使指定了此标志，仍可能需要附加权限才能够访问该文件。**ReadWrite**：允许随后打开文件读取或写入。如果未指定此标志，则文件关闭前，任何打开该文件以进行读取或写入的请求（由此进程或另一进程发出）都将失败。但是，即使指定了此标志，仍可能需要附加权限才能够访问该文件。**Write**：允许随后打开文件写入。如果未指定此标志，则文件关闭前，任何打开该文件以进行写入的请求（由此进程或另一进过程发出的请求）都将失败。但是，即使指定了此标志，仍可能需要附加权限才能够访问该文件。**Delete**：允许随后删除文件。 |

#### 文本文件的读写

> **StreamReader** 和 **StreamWriter** 类用于文本文件的数据读写
>
> 这些类从抽象基类 Stream 继承，Stream 支持文件流的字节读写

##### StreamReader 类

> **StreamReader** 类继承自抽象基类 TextReader，表示阅读器读取一系列字符

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public override void Close()** 关闭 StreamReader 对象和基础流，并释放任何与读者相关的系统资源。 |
| 2    | **public override int Peek()** 返回下一个可用的字符，但不使用它。 |
| 3    | **public override int Read()** 从输入流中读取下一个字符，并把字符位置往前移一个字符。 |

##### StreamWriter 类

> **StreamWriter** 类继承自抽象类 TextWriter，表示编写器写入一系列字符

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public override void Close()** 关闭当前的 StreamWriter 对象和基础流。 |
| 2    | **public override void Flush()** 清理当前编写器的所有缓冲区，使得所有缓冲数据写入基础流。 |
| 3    | **public virtual void Write(bool value)** 把一个布尔值的文本表示形式写入到文本字符串或流。（继承自 TextWriter。） |
| 4    | **public override void Write( char value )** 把一个字符写入到流。 |
| 5    | **public virtual void Write( decimal value )** 把一个十进制值的文本表示形式写入到文本字符串或流。 |
| 6    | **public virtual void Write( double value )** 把一个 8 字节浮点值的文本表示形式写入到文本字符串或流。 |
| 7    | **public virtual void Write( int value )** 把一个 4 字节有符号整数的文本表示形式写入到文本字符串或流。 |
| 8    | **public override void Write( string value )** 把一个字符串写入到流。 |
| 9    | **public virtual void WriteLine()** 把行结束符写入到文本字符串或流。 |

##### BinaryReader 类

> **BinaryReader** 类用于从文件读取二进制数据
>
> 一个 **BinaryReader** 对象通过向它的构造函数传递 **FileStream** 对象而被创建

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public override void Close()** 关闭 BinaryReader 对象和基础流。 |
| 2    | **public virtual int Read()** 从基础流中读取字符，并把流的当前位置往前移。 |
| 3    | **public virtual bool ReadBoolean()** 从当前流中读取一个布尔值，并把流的当前位置往前移一个字节。 |
| 4    | **public virtual byte ReadByte()** 从当前流中读取下一个字节，并把流的当前位置往前移一个字节。 |
| 5    | **public virtual byte[] ReadBytes( int count )** 从当前流中读取指定数目的字节到一个字节数组中，并把流的当前位置往前移指定数目的字节。 |
| 6    | **public virtual char ReadChar()** 从当前流中读取下一个字节，并把流的当前位置按照所使用的编码和从流中读取的指定的字符往前移。 |
| 7    | **public virtual char[] ReadChars( int count )** 从当前流中读取指定数目的字节，在一个字符数组中返回数组，并把流的当前位置按照所使用的编码和从流中读取的指定的字符往前移。 |
| 8    | **public virtual double ReadDouble()** 从当前流中读取一个 8 字节浮点值，并把流的当前位置往前移八个字节。 |
| 9    | **public virtual int ReadInt32()** 从当前流中读取一个 4 字节有符号整数，并把流的当前位置往前移四个字节。 |
| 10   | **public virtual string ReadString()** 从当前流中读取一个字符串。字符串以长度作为前缀，同时编码为一个七位的整数。 |

##### BinaryWriter 类

> **BinaryWriter** 类用于向文件写入二进制数据
>
> 一个 **BinaryWriter** 对象通过向它的构造函数传递 **FileStream** 对象而被创建

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public override void Close()** 关闭 BinaryWriter 对象和基础流。 |
| 2    | **public virtual void Flush()** 清理当前编写器的所有缓冲区，使得所有缓冲数据写入基础设备。 |
| 3    | **public virtual long Seek( int offset, SeekOrigin origin )** 设置当前流内的位置。 |
| 4    | **public virtual void Write( bool value )** 把一个单字节的布尔值写入到当前流中，0 表示 false，1 表示 true。 |
| 5    | **public virtual void Write( byte value )** 把一个无符号字节写入到当前流中，并把流的位置往前移一个字节。 |
| 6    | **public virtual void Write( byte[] buffer )** 把一个字节数组写入到基础流中。 |
| 7    | **public virtual void Write( char ch )** 把一个 Unicode 字符写入到当前流中，并把流的当前位置按照所使用的编码和要写入到流中的指定的字符往前移。 |
| 8    | **public virtual void Write( char[] chars )** 把一个字符数组写入到当前流中，并把流的当前位置按照所使用的编码和要写入到流中的指定的字符往前移。 |
| 9    | **public virtual void Write( double value )** 把一个 8 字节浮点值写入到当前流中，并把流位置往前移八个字节。 |
| 10   | **public virtual void Write( int value )** 把一个 4 字节有符号整数写入到当前流中，并把流位置往前移四个字节。 |
| 11   | **public virtual void Write( string value )** 把一个以长度为前缀的字符串写入到 BinaryWriter 的当前编码的流中，并把流的当前位置按照所使用的编码和要写入到流中的指定的字符往前移。 |

##### DirectoryInfo 类

> **DirectoryInfo** 类派生自 **FileSystemInfo** 类
>
> 它提供了各种用于创建、移动、浏览目录和子目录的方法
>
> 该类不能被继承

| 序号 | 属性 & 描述                                             |
| :--- | :------------------------------------------------------ |
| 1    | **Attributes** 获取当前文件或目录的属性。               |
| 2    | **CreationTime** 获取当前文件或目录的创建时间。         |
| 3    | **Exists** 获取一个表示目录是否存在的布尔值。           |
| 4    | **Extension** 获取表示文件存在的字符串。                |
| 5    | **FullName** 获取目录或文件的完整路径。                 |
| 6    | **LastAccessTime** 获取当前文件或目录最后被访问的时间。 |
| 7    | **Name** 获取该 DirectoryInfo 实例的名称。              |

> 下表列出了 **DirectoryInfo** 类中一些常用的**方法**

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public void Create()** 创建一个目录。                      |
| 2    | **public DirectoryInfo CreateSubdirectory( string path )** 在指定的路径上创建子目录。指定的路径可以是相对于 DirectoryInfo 类的实例的路径。 |
| 3    | **public override void Delete()** 如果为空的，则删除该 DirectoryInfo。 |
| 4    | **public DirectoryInfo[] GetDirectories()** 返回当前目录的子目录。 |
| 5    | **public FileInfo[] GetFiles()** 从当前目录返回文件列表。    |

##### FileInfo 类

> **FileInfo** 类派生自 **FileSystemInfo** 类
>
> 它提供了用于创建、复制、删除、移动、打开文件的属性和方法，且有助于 FileStream 对象的创建
>
> 该类不能被继承
>
> 下表列出了 **FileInfo** 类中一些常用的**属性** :

| 序号 | 属性 & 描述                                       |
| :--- | :------------------------------------------------ |
| 1    | **Attributes** 获取当前文件的属性。               |
| 2    | **CreationTime** 获取当前文件的创建时间。         |
| 3    | **Directory** 获取文件所属目录的一个实例。        |
| 4    | **Exists** 获取一个表示文件是否存在的布尔值。     |
| 5    | **Extension** 获取表示文件存在的字符串。          |
| 6    | **FullName** 获取文件的完整路径。                 |
| 7    | **LastAccessTime** 获取当前文件最后被访问的时间。 |
| 8    | **LastWriteTime** 获取文件最后被写入的时间。      |
| 9    | **Length** 获取当前文件的大小，以字节为单位。     |
| 10   | **Name** 获取文件的名称。                         |

下表列出了 **FileInfo** 类中一些常用的**方法** :

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **public StreamWriter AppendText()** 创建一个 StreamWriter，追加文本到由 FileInfo 的实例表示的文件中。 |
| 2    | **public FileStream Create()** 创建一个文件。                |
| 3    | **public override void Delete()** 永久删除一个文件。         |
| 4    | **public void MoveTo( string destFileName )** 移动一个指定的文件到一个新的位置，提供选项来指定新的文件名。 |
| 5    | **public FileStream Open( FileMode mode )** 以指定的模式打开一个文件。 |
| 6    | **public FileStream Open( FileMode mode, FileAccess access )** 以指定的模式，使用 read、write 或 read/write 访问，来打开一个文件。 |
| 7    | **public FileStream Open( FileMode mode, FileAccess access, FileShare share )** 以指定的模式，使用 read、write 或 read/write 访问，以及指定的分享选项，来打开一个文件。 |
| 8    | **public FileStream OpenRead()** 创建一个只读的 FileStream。 |
| 9    | **public FileStream OpenWrite()** 创建一个只写的 FileStream。 |
