# C#高级玩法

## 概述

[TOC]

## 泛型

### 为什么用泛型集合

![image-20230313232641543](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303132326590.png)

### 泛型集合

![image-20230313232740422](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303132327476.png)

![image-20230313234307014](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303132343555.png)

### Dictionary

![image-20230314140529248](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141405291.png)

#### 遍历字典

![image-20230314142125605](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141421639.png)

#### 排序

![image-20230314143817567](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141438609.png)

#### 排序多个参数的对象

- 升序排序other在前，this在后
- 大于0，前者 > 后者

![image-20230314145226523](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141452559.png)

#### 动态排序

> 利用比较器ICompare<T>（排序类），分别实现排序接口，和cpp类似

![](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141511527.png)

- 如何使用

![](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141541937.png)

## Winform窗体

### B/S架构

![image-20230314154838911](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141548984.png)

### C/S架构

![image-20230314154920890](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141549979.png)

### 窗体类

![image-20230314162537629](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303141625673.png)

- partial关键字

> 将几个partial修饰的类，定义为一个类

### 事件驱动机制