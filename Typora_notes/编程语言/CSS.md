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



### 后代选择器

- 作用：选中指定元素中，符合要求的后代元素。
- 语法：选择器1 选择器2 选择器3 ...... 选择器n {} （先写祖先，再写后代）  

> 选择器之间，用空格隔开，空格可以理解为：" xxx 中的"，其实就是后代的意思。
> 选择器 1234....n ，可以是我们之前学的任何一种选择器。

> 几种关系：
>
> - 父元素
>
> - 子元素
>
> - 祖先元素
>
> - 后代元素
>
> - 兄弟元素

  



> 后代选择器，可以用复合选择器组合出来
>
> 重点：
>
> 1.  .class  ：类
> 2.  #id      ：id
> 3.  label    ： 标签

- 举例

```css
/* 选中ul中的所有li */
ul li {
	color: red;
}

/* 选中ul中所有li中的a */
ul li a {
	color: orange;
}

/* 选中类名为subject元素中的所有li */
.subject li {
	color: blue;
}

/* 选中类名为subject元素中的所有类名为front-end的li */
.subject li.front-end {
	color: blue;
}
```



> notes：
>
> 注意：
>
> 1. 后代选择器，最终选择的是后代，不选中祖先。
> 2. 儿子、孙子、重孙子，都算是后代。
> 3. 结构一定要符合之前讲的 HTML 嵌套要求，例如：不能 p 中写 h1 ~ h6   





### 子代选择器

- 作用：选中指定元素中，符合要求的子元素（儿子元素）。（先写父，再写子）
- 语法：选择器1 > 选择器2 > 选择器3 > ...... 选择器n {}  

> 选择器之间，用 > 隔开， > 可以理解为：" xxx 的子代"，其实就是儿子的意思。
> 选择器 1234....n ，可以是我们之前学的任何一种选择器。  

- 举例

```css
/* div中的子代a元素 */
div>a {
	color: red;
} 
/* 类名为persons的元素中的子代a元素 */
.persons>a{
	color: red;
}
```

> notes：
>
> 注意：
>
> 1. 子代选择器，最终选择的是子代，不是父级。
> 2. 子、孙子、重孙子、重重孙子 ...... 统称后代！，子就是指儿子。  



### 兄弟选择器

> 选择兄弟器，此时123为红色

```css
    <title>兄弟选择器</title>
    <style>
        div+p+p {
            color: red;
        }
    </style>

    <div>football</div>
    <p>nihao</p>
    <p>123</p>
    <p>abc</p>
```

> 只往下寻找，123为红色

```css
    <title>兄弟选择器</title>
    <style>
        div+p {
            color: red;
        }
    </style>

    
    <p>nihao</p>
	<div>football</div>
    <p>123</p>
    <p>abc</p>
```

> 相邻兄弟选择器，只能是仅仅相邻的p，h1不变红色

```css
    <title>相邻兄弟选择器</title>
    <style>
        div+p {
            color: red;
        }
    </style>

    <div>football</div>
	<H1>HELLO></H1>
    <p>nihao</p>
    <p>123</p>
    <p>abc</p>
```

> 通用兄弟选择器，选中后面所有的兄弟

```css
    <title>通用兄弟选择器</title>
    <style>
        div~p {
            color: red;
        }
    </style>

    <div>football</div>
	<H1>HELLO></H1>
    <p>nihao</p>
    <p>123</p>
    <p>abc</p>
```



### 属性选择器

- 作用：选中属性值符合一定要求的元素。
- 语法：

1. [属性名] 选中==具有==某个属性的元素。
2. [属性名="值"] 选中包含某个属性，且属性值==等于==指定值的元素。
3. [属性名^="值"] 选中包含某个属性，且属性值以指定的值==开头==的元素。
4. [属性名$="值"] 选中包含某个属性，且属性值以指定的值==结尾==的元素。
5. [属性名*=“值”] 选择包含某个属性，属性值==包含==指定值的元素。  



> 选择带有title属性的元素，全红

```css
    <style>
        [title] {
            color: red;
        }
    </style>

    <div title="abc1">football</div>
    <div title="abc2">ball</div>
    <div title="abc3">foot</div>
    <div title="abc4">bullet</div>
```

> 选择带有title = abc2 的元素，abc2红

```css
    <style>
        [title = “abc2”] {
            color: red;
        }
    </style>

    <div title="abc1">football</div>
    <div title="abc2">ball</div>
    <div title="abc3">foot</div>
    <div title="abc4">bullet</div>
```

> 选择带有title的值开头为a的元素，title=xxx1 不变红

```css
    <style>
        [title^="abc"] {
            color: red;
        }
    </style>

    <div title="abc1">football</div>
    <div title="abc2">ball</div>
    <div title="abc3">foot</div>
    <div title="abc4">bullet</div>
    <div title="xxx1">bullet</div>

```

> 选择title的值以1结尾的元素，football 和 habby 变红

```css
    <style>
        [title$="1"] {
            color: red;
        }
    </style>
    <div title="abc1"> football </div>
    <div title="abc2"> ball </div>
    <div title="abc3"> foot </div>
    <div title="abc4"> bullet </div>
    <div title="xxx1"> habby </div>
```

> 选择title的值 包含 1 的元素，football 和 habby 变红

```css
    <style>
        [title*="1"] {
            color: red;
        }
    </style>
    <div title="abc1"> football </div>
    <div title="abc2"> ball </div>
    <div title="abc3"> foot </div>
    <div title="abc4"> bullet </div>
    <div title="xxx1"> habby </div>
```



### 伪类选择器

> 作用：选中特殊状态的元素。  

- 动态伪类 ()
    - :link 超链接==未被访问==的状态。
    - :visited 超链接==访问过==的状态。
    - :hover 鼠标==悬停==在元素上的状态
    - :active 元素==激活==的状态  
- 结构伪类
    - 