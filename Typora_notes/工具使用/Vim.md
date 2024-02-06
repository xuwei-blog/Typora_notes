# Vim

[TOC]

> 课程来源:[2-2 Vim，为什么你有这么多模式_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1NG4y1p74h/?p=3&spm_id_from=pageDriver&vd_source=91ddf1aeb53bd3336e78168da8d0b7dd)

## 简介

> - 学习Vim流程
>
> 1. 移动、增删改查
> 2. 配置Vim，编写vimrc文件
> 3. 安装插件，扩充Vim功能
>
> - 三种模式
>
> 1. 普通模式    Esc
> 2. 输入模式    
>     - i    ： insert 
>     - a   ： append 
>     - o   ： open a line below
>     - I    ： insert before line
>     - A   ： append after line
>     - O   ： append a line above
> 3. 命令模式
>     -    :    



## 普通模式基操

### 可视模式

- normal模式下使用v进入visual选择
- 使用V选择行
- 使用ctrl+v进行方块选择

### 移动方向键

```
	  ^
	  k
< h       l >
	  j
	  v
```

### 单词之间移动

- w/W：移动到下一个word/WORD开头
- e/E： 移动到下一个word/WORD结尾
- b/B：移动到上一个word/WORD开头
- word：非空白符分割的单词
- WORD：空白符分割的单词

### 行间搜索移动

- 使用  f{char}   可以移动到char字符上
- 使用  t{char}   可以移动到char字符前
- 大写F，往前搜

### 水平移动

- 0移动到行首第一个字符，^移动到第一个非空白字符
- $移动到行尾，g_移动到行尾非空白字符
- 重点记忆 0  和   $ 



### 页面移动

- gg / G 移动到文件开头和结尾
- H：开头
- M：中间
- L：结尾
- ctrl + o 快速返回

### 翻页

- ctrl + u ：向上翻页
- ctrl + f ： 向下翻页
- zz：把屏幕放中间

### 快速删除

- daw：delete around word

- diw

- dd：删除一行

- det：删除

- x：快速删除一个字符

- 5x：删除5个字符

    

### 修改命令，常用caw

- r：replace
- c：change     （  ct”，删除到“  ） （cw  、caw，修改单词）
- s：substitute   （ 4s  ）

### 撤销

- u：undo

### 查询

- 使用 /  或者 ？ 向前或向后搜索
- n/N  跳转到下一个或者上一个匹配
- 使用 * 或者 # 进行当前单词的前后匹配

### 替换

- range表示范围 
- flags常用标志
    - g global表示全局范围内执行
    - c confirm表示确认，可以确定或者拒绝修改
    - n number报告匹配的次数而不替换，可以用来查询匹配次数
- 语法格式

```
:[range]S[substitute]/{pattern}/{string}/[flags]
:1,6 S/pro/cur/g  # 1~6行，pro替换成cur ，全局
```



## 输入模式基操

### 快速纠错

- ctrl+h：删除上一个字符
- ctrl+w：删除上一个单词
- ctrl+u：删除当前行

### 快速切换 insert模式~normal模式

- ctrl+c：可能会中断某些插件
- ctrl+[：更推荐使用

### 快速切换 normal模式~insert模式

- gi：快速切换到最后一次编辑的位置，并进行编辑

## 命令模式基操

- 保存

```
:w
```

- 退出

```
:q
```

- 分屏

```
:vs（vertical split）
```

```
:sp（split）
```

- 全局替换

```
:% s/foo/bar/g 全局替换
```

- 设置行号

```
:set nu
```

