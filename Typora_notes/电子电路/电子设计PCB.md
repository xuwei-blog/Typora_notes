# 电子设计PCB

## 概述

[TOC]

软件：AD22

课程：B站凡亿教育

## 软件操作流程

1. 新建工程
2. 新建原理图库
3. 新建原理图
4. 新建PCB元件库
5. 新建PCB

> 注意：
>
> 1. 文件唯一性
>
>  ![image-20230227211651636](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302272116671.png)
>
> 2. 如何打开工程文件？避免游离文件
>
> ![image-20230227211632916](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302272116050.png)

## 原理图库的创建

### 元件符号

![image-20230227212015075](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302272120113.png)

#### 元件ID

> 1. 电容----------》CAP
> 2. 电阻----------》RES
> 3. 发光二极管-》LED
> 4. 二极管-------》DIO

### 创建原理图库

1. 双击Schlib，创建电容、电阻

![image-20230227215159666](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302272151693.png)

2. 设置格栅

![image-20230227220146809](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302272201846.png)

3. 绘制元件

![image-20230227220759251](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302272207310.png)

### 二极管的绘制

1. 利用多边形



### 运算放大器的绘制

- 编辑-移动-放到后面（不要隐藏引脚的名字）

![image-20230227222601569](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302272226606.png)

### 多part部件

- 工具 - 新部件



### 调用他人的原理图库

1. 已有的原理图进行生成
2. PCB联盟网 - 搜索 - PCB超级库
3. IC封装网
4. 复制现有的库

### 检查原理图库正确性

- 报告 - 器件规则检查

![image-20230228115005616](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281150686.png)

### 原理图页的设置

- 原理图 - 双击边缘 - 设置画幅

### 器件的摆放

- Panels - Components - 设置预览 - 拖动

### 元件的复制、剪切、旋转、镜像

- 复制
  - 按shift拖动
  - CV
- 旋转
  - 拖动并按空格

- 剪切
  - ctrl+ X
- 镜像
  - 拖动并按 X 左右镜像
  - 拖动并按 Y 上下镜像

### 元件的对齐

- 选中后 - 右键 - 对齐

### 走线（放置导线）

- 放置 - 线 （切记不要用画图的线，因为没有导线属性）

### 网络标签

- 放置 - 网络标签

![image-20230228130353056](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281303103.png)

> 对于电源和地的连接，采用特殊的网络标号-VCC、GND

### 非电气对象的放置（辅助线、文字）

![image-20230228132736250](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281327291.png)

- 调整后得到

![image-20230228133418816](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281334928.png)

### 元器件编号

- 工具 - 标注 - 原理图标注

![image-20230228142025627](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281420706.png) 

> 1. 先取消标号（可以全选 右键 解锁全部标记）
> 2. 选择处理顺序
>
> ![image-20230228143732045](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281437080.png)
>
> 3. 更新更改列表
> 4. 接收更改
> 5. 执行变更

### 查找元件

- J - C - 元件名字

### 原理图编译与检查

- 避免网络悬浮
  - 网络标签 左下角 的点 要连在线上 
- 避免重复元件位号
  - 尽量不要手动修改
- 避免悬浮电源端口
- 避免单端网络
  - 网络标号 成队 出现

> 设置报错等级（已经设置）

> 处理报错
>
> 1. 如果要保留单端网络，就设置no ERC
>
> - 放置 - 指示 - No ERC
>
> 2. off grid 不在栅格上

### BOM物料表

> - 报告 - BOM - 修改导出信息 Columns - 导出
> - 原理图出来后，就可以整理BOM表了，不需要等PCB也弄完

### 导出原理图PDF

- 文件 - 智能PDF

### 原理图快捷键

> 自定义快捷键
>
> 1. 按住CTRL 对着想修改的操作名 按左键

#### 视图快捷键

![image-20230228154448906](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281548332.png)

#### 排列对齐快捷键

![image-20230228154558594](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281548009.png)





## PCB的创建

### PCB封装的组成

![image-20230228174514818](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281745867.png)

> - 通孔焊盘
>
> ![image-20230228174644875](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281746921.png)
>
> 2. 表贴焊盘![image-20230228174748878](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281747914.png)
> 3. 紫色防止油墨覆盖，绿色是阻焊绿油

- 封装步骤

1. 先封装两个焊盘

![image-20230228181120686](C:\Users\13192\AppData\Roaming\Typora\typora-user-images\image-20230228181120686.png)

2. 丝印层的走线

![image-20230228181814347](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281818397.png)

3. 为了保证丝印不被油墨挡住

![image-20230228182145564](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281821609.png)



### 异形焊盘

> 操作方法
>
> 1. 更改属性
> 2. 叠加焊盘
> 3. 在PCB文件作画 工具 - 转换 - 从选择的元素创建区域

1. 用 `线` 画出 弧线 ，并将区域设置为 top layer

![image-20230228184539135](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281845200.png)

2. 通过叠加焊盘搞出==管脚号==

![image-20230228184659238](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281846288.png)

3. 设置规则 - 最小间距2.5mil 

4. 工具 - ==描绘选择对象的外形== - 删除内部外形 - 外部外形设置为1mil
5. 再次绘制区域 - 并设为top solder

6. 在top overlay 画 ==丝印==

![image-20230228185235332](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202302281852378.png)

7. 最后==复制到PCB库==

- 方法2 ：两个重叠的区域，==改粗==一个区域的边缘线条，多的