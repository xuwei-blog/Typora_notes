# CSS

[TOC]

> 心得：
>
> 1. CSS美化HTML
> 2. HTML搭建结构，CSS添加样式，结构和样式分离

## 简介

- 概念

> CSS：层叠样式表 cascading style sheets
>
> CSS也是一种标记语言，用于给HTML结构设置样式，例如，文字大小、颜色、元素宽高



- 行内样式 (内联样式)

> 属性style的值，符合CSS的格式，属性  :  值  ;
>
> 结构 和 样式 混在一起，不便于维护，不推荐以下方式

```html
<h1 style="color: red;">hello</h1>
<h1 style="color: red;font-size: 10px;">hello</h1>
```



- 内部样式

> style标签，内部要遵循CSS规范，一般要将style放在头标签内
>
> css一定要写px，在html中，10px可以简写成10
>
> 结构 和 样式 没有完全分离，style仍然写在 .html里

```html
<head>
    <meta charset="UTF-8">
    <title>内部样式</title>
    
    <style>
        h1{
            color: green;
            font-size: 10px;
        }
        h2{
            color: red;
            font-size: 40px;
        }
    </style>
    
</head>
<body>
    <h1>hello</h1>
    <h2>baibai</h2>
</body>
```



- 外部样式

> 结构 和 样式 ， 完全分离
>
> 以下是css文件

```css
h1{
    color: green;
    font-size: 10px;
}
h2{
    color: red;
    font-size: 40px;
}
```

> 源html的链接

```html
<head>
    <title>外部样式</title>
    <link rel="stylesheet" href="./test.css">
</head>
```



- 优先级

> 行内样式	>	内部样式	=	外部样式
>
> 内部样式 和 外部样式 ，写在后面的会 覆盖 前面的



- 语法规范

> 细节：
>
> 1. 最后一个声明块的 ；可以省略
> 2. 选择器 与 声明块 之间有空格
> 3. 声明的 ： 后面有空格
> 4. 注释   ：       /*  */

![image-20231212133757411](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202312121337500.png)



- 代码风格

> 1. 展开风格
>
>     ```html
>     <style>
>         h1{
>             color: red;
>             font-size: 10px;
>         }
>     </style>
>     ```
>
> 2. 紧凑风格 (节约文件体积)
>
>     ```html
>     <style>
>         h1{color:red;font-size:10px;}
>     </style>
>     ```



## 选择器

### 基本选择器

> 基本选择器类别：
>
> 1. 通配选择器
> 2. 元素选择器
> 3. 类选择器
> 4. id 选择器



- 通配选择器

> 1. 可以选中所有HTML元素
> 2. 清除样式时，有很大作用

```html
* {
	color: red;
}
```



- 元素选择器

> 1. 页面上所有的h1 标签都改为红色

```html
h1 {
	color: red;
}
```



- 类选择器

> 1. 因为元素选择器不能 差异化 同类标签的样式
> 2. 一个元素不能有多个同名属性 ， 只有第一个会生效
> 3. 一个标签有1个class属性，但可以有多个class 值 (类名)，类名用空格分隔

```html
<head>
    <title>类选择器</title>
    <style>
        .speak {
            color: red;
        }
        .ans {
            color: green;
        }
        .big{
            font-size: 90px;
        }
    </style>

</head>

<body>

    <h1 class="speak">我说：hello</h1>
    <p class="speak">我说：hello</p>

    <h2 class="ans big">你说：goodbye</h2>
    <p class="ans">你说：goodbye</p>
</body>
```



- id 选择器

> 1. id 不能数字开头
> 2. 不能在本页面有重复的id
> 3.  id 和 class 可以同时存在

```html
<head>
    <meta charset="UTF-8">
    <title>id 选择器</title>
    <style>
        #woshuo {
            color: blue;
        }
        #nishuo {
            color: red;
        }
    </style>

</head>
<body>
    <p id="woshuo">我说：hello</p>

    <p id="nishuo">你说：goodbye</p>
</body>
```



### 复合选择器

> 复合选择器的种类：
>
> 1.  交集选择器
> 2. 并集选择器



- 交集选择器

```html
<head>
    <meta charset="UTF-8">
    <title>交集选择器</title>
    <style>
        p.animal {
            color: red;
        }
        .animal.female {
            font-size: 20px;
        }
    </style>

</head>
<body>

    <h1 class="animal">老王</h1>
    <h2 class="female">老张</h2>

    <p class="animal">小狗</p>
    <p class="animal">小猪</p>
</body>
```



- 并集选择器

```html
<head>
    <meta charset="UTF-8">
    <title>并集选择器</title>
    <style>
        .cla1,
        .cla2,
        .cla4,
        #xiaoyang {
            color: red;
        }
    </style>

</head>
<body>

    <h1 class="cla1">老王</h1>
    <h2 class="cla2">老张</h2>

    <p class="cla3">小狗</p>
    <p class="cla4">小猪</p>
    <p id="xiaoyang">小羊</p>
</body>
```



- 父元素

![image-20231212151613997](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202312121516085.png)



- 子元素

![image-20231212151728057](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202312121517293.png)



- 祖先元素

![image-20231212151928541](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202312121519608.png)



- 后代元素

![image-20231212152028059](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202312121520225.png)



- 兄弟元素

![image-20231212152321885](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202312121523964.png)