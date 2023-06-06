# makefile使用指南

## 概述

[TOC]

## 新手须知

### 基本格式

```makefile
targets : prerequisties
[tab键]command
```

- target：目标文件，可以是 OjectFile，也可以是执行文件，还可以是一个标签（Label），对于标签这种特性，在后续的“伪目标”章节中会有叙述。
- prerequisite：要生成那个 target 所需要的文件或是目标。
- command：是 make 需要执行的命令

### 规则

- make 会在当前目录下找到一个名字叫 `Makefile` 或 `makefile` 的文件
- 如果找到，它会找文件中第一个目标文件（target），并把这个文件作为最终的目标文件
- 如果 target 文件不存在，或是 target 文件依赖的 .o 文件(prerequities)的文件修改时间要比 target 这个文件新，就会执行后面所定义的命令 command 来生成 target 这个文件      
- 如果 target 依赖的 .o 文件（prerequisties）也存在，make 会在当前文件中找到 target 为 .o 文件的依赖性，如果找到，再根据那个规则生成 .o 文件

### 伪目标

"伪目标" 不是一个文件，只是一个标签。我们要显示地指明这个 "目标" 才能让其生效

"伪目标" 的取名不能和文件名重名，否则不会执行命令

为了避免和文件重名的这种情况，我们可以使用一个特殊的标记 `.PHONY` 来显示地指明一个目标是“伪目标”，向 make 说明，不管是否有这个文件，这个目标就是 "伪目标"

```makefile
.PHONY : clean
```

只要有这个声明，不管是否有“clean”文件，要运行 "clean" 这个目标，只有"make clean" 这个命令



## 变量

### 变量的定义

```makefile
cpp := src/main.cpp 
obj := objs/main.o
```

### 变量的引用

- 可以用 `()` 或 `{}`

```makefile
cpp := src/main.cpp 
obj := objs/main.o

$(obj) : ${cpp}
	@g++ -c $(cpp) -o $(obj)

compile : $(obj)
```

### 预定义变量

- `$@`: 目标(target)的完整名称
- `$<`: 第一个依赖文件（prerequisties）的名称
- `$^`: 所有的依赖文件（prerequisties），以空格分开，不包含重复的依赖文件

```makefile
cpp := src/main.cpp 
obj := objs/main.o

$(obj) : ${cpp}
	@g++ -c $< -o $@
	@echo $^

compile : $(obj)
.PHONY : compile
```



## 等号、续行符

### =

- 简单的赋值运算符
- 用于将右边的值分配给左边的变量
- 如果在后面的语句中重新定义了该变量，则将使用新的值

>示例

```makefile
HOST_ARCH   = aarch64
TARGET_ARCH = $(HOST_ARCH)

# 更改了变量 a
HOST_ARCH   = amd64

debug:
	@echo $(TARGET_ARCH)
```

> make debug
>
> \>>>
>
> amd64



### :=

- 立即赋值运算符
- 用于在定义变量时立即求值
- 该值在定义后不再更改
- 即使在后面的语句中重新定义了该变量

>示例

```makefile
HOST_ARCH   := aarch64
TARGET_ARCH := $(HOST_ARCH)

# 更改了变量 a
HOST_ARCH := amd64

debug:
	@echo $(TARGET_ARCH)
```

> make debug
>
> \>>>
>
> aarch64


### ?=

- 默认赋值运算符
- 如果该变量已经定义，则不进行任何操作
- 如果该变量尚未定义，则求值并分配

```makefile
HOST_ARCH  = aarch64
HOST_ARCH ?= amd64

debug:
    @echo $(HOST_ARCH)
```

### +=

```makefile
include_paths = src

CXXFLAGS := -m64 -fPIC -g -O0 -std=c++11 -w -fopenmp

CXXFLAGS += $(include_paths)
```

> make CXXFLAGS
>
> \>>>
>
> -m64 -fPIC -g -O0 -std=c++11 -w -fopenmp src

### \

- 续行符

>示例

```make
LDLIBS := cudart opencv_core \
          gomp nvinfer protobuf cudnn pthread \
          cublas nvcaffe_parser nvinfer_plugin 
```







## 常用函数

### 函数语法

函数调用，很像变量的使用，也是以 “$” 来标识的，其语法如下：

```makefile
$(fn, arguments) or ${fn, arguments}
```

- fn: 函数名
- arguments: 函数参数，参数间以逗号 `,` 分隔，而函数名和参数之间以“空格”分隔



### shell

```makefile
$(shell <command> <arguments>)
```

- 名称：shell 命令函数 —— shell
- 功能：调用 shell 命令 command
- 返回：函数返回 shell 命令 command 的执行结果


>示例

```makefile
# shell 指令，src 文件夹下找到 .cpp 文件
cpp_srcs := $(shell find src -name "*.cpp") 
# shell 指令, 获取计算机架构
HOST_ARCH := $(shell uname -m)
```

> 查找文件夹内的.cpp后缀文件

![image-20230527112830548](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305271128737.png)

### subst

```makefile
$(subst <from>,<to>,<text>)
```

- 名称：字符串替换函数——subst
- 功能：把字串 \<text> 中的 \<from> 字符串替换成 \<to>
- 返回：函数返回被替换过后的字符串

>示例：

```makefile
cpp_srcs := $(shell find src -name "*.cpp")
cpp_objs := $(subst src/,objs/,$(cpp_objs)) 

```

> 类似一个ti'huan

![image-20230527114017186](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305271140242.png)

### patsubst

```makefile
$(patsubst <pattern>,<replacement>,<text>)
```

- 名称：模式字符串替换函数 —— patsubst
- 功能：通配符 `%`，表示任意长度的字串，从 text 中取出 patttern， 替换成 replacement
- 返回：函数返回被替换过后的字符串

>示例

```makefile
cpp_srcs := $(shell find src -name "*.cpp") #shell指令，src文件夹下找到.cpp文件
cpp_objs := $(patsubst %.cpp,%.o,$(cpp_srcs)) #cpp_srcs变量下cpp文件替换成 .o文件
```

### foreach

```makefile
$(foreach <var>,<list>,<text>)
```

- 名称：循环函数——foreach。
- 功能：把字串\<list>中的元素逐一取出来，执行\<text>包含的表达式
- 返回：\<text>所返回的每个字符串所组成的整个字符串（以空格分隔）

>示例：

```makefile
library_paths := /datav/shared/100_du/03.08/lean/protobuf-3.11.4/lib \
                 /usr/local/cuda-10.1/lib64 \

library_paths := $(foreach item,$(library_paths),-L$(item))
```

>同等效果

```makefile
I_flag := $(include_paths:%=-I%)
```



### dir

```makefile
$(dir <names...>)
```

- 名称：取目录函数——dir。
- 功能：从文件名序列<names>中取出目录部分。目录部分是指最后一个反斜杠（“/”）之前
  的部分。如果没有反斜杠，那么返回“./”。
- 返回：返回文件名序列<names>的目录部分。
- 示例： 

```makefile
$(dir src/foo.c hacks)    # 返回值是“src/ ./”。
```

> 实例

![image-20230527115615650](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305271156708.png)

### notdir

> 保留文件名，去除目录

```makefile
$(notdir <names...>)
```

>示例

```makefile
libs   := $(notdir $(shell find /usr/lib -name lib*)
```

### filter

> 根据特征 取出 内容

```makefile
$(filter <names...>)
```

```makefile
libs    := $(notdir $(shell find /usr/lib -name lib*))
a_libs  := $(filter %.a,$(libs))
so_libs := $(filter %.so,$(libs))
```



### basename

> 去除后缀
>

```makefile
$(basename <names...>)
```

```makefile
libs    := $(notdir $(shell find /usr/lib -name lib*))
a_libs  := $(subst lib,,$(basename $(filter %.a,$(libs))))
so_libs := $(subst lib,,$(basename $(filter %.so,$(libs))))
```



## 编译

### 预处理

### 编译

### 汇编

### 链接

### 编译选项

### 编译带头文件的程序

### 链接静态库

## 有需要再学习！！！

