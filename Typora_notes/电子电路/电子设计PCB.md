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

> CTRL + d     切换3D
>
> 按住shift+右键   ==》  旋转查看

> CTRL + q     切换单位

> shift + e     切换自动吸附

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

![image-20230228181120686](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012116073.png)

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



### IPC封装向导

1. 工具 - IPC(CFW)
2. 选封装排列方式

2. 根据器件的尺寸图填入

![image-20230301144942350](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303011628459.png)

2. 取消散热焊盘
3. 根据IPC行业标准，稍微补偿一下数据
4. 根据焊盘布局，挑选焊盘的密度（默认折中）
5. 后面一般都一路next

### 复制别人的PCB

1. 直接复制别人的PCB库
2. PCB文件 - 设计 - 生产PCB库 - 将生成的PCB库复制到自己的PCB库
3. PCB联盟网 - PCB超级库
4. IC封装网

### PCB封装的检测

![image-20230301154502183](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303011628036.png)

> 步骤：
>
> 1. 打开PCB库 - 报告 - 元件规则检查
> 2. 根据报错，来修复错误

### 3D PCB封装

> 可以自己画3D
>
> 也可以导入现成的 放置 - 3D体 - 选3D模型



1. 放置 - 3D元件体
2. 绕着丝印层画一圈 并将属性改为 机械1层

![image-20230301160116978](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303011628958.png)

3. 查阅资料，修改线高

![image-20230301160356778](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303011628860.png)

4. 修改完后，更新到PCB

![image-20230301161534504](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303011628993.png)

### PCB板框与DXF导入

> 把PCB的器件框起来
>
> 定义板框
>
> 注意：板框的边线长度为整数

![image-20230301203059263](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012030362.png)



> 按照结构工程师的CAD图来做板框
>
> CAD导出DXF2004版本文件
>
> 在打开DXF放到机械二层
>
> 复制CAD边框，编辑 - 特殊粘贴到机械一层

![image-20230301204251387](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012042447.png)

> 挖掉内部凹槽（定位孔）

![image-20230301204311306](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012043380.png)



### 固定孔和器件的精准定位

#### 自定义固定孔

> 固定孔一般 盘和孔 等大，且 非金属

![image-20230301204958168](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012049238.png)

> 将板框左下角设为原点 - X、Y位移 固定孔

![image-20230301205342694](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012053768.png)

#### 更改导入板框的定位孔

> 放置焊盘 - 调整大小 - 非金属 

### 层叠

> 设计 - 层叠管理器
>
> 注意：为了不让软件自动添加层，把√取消了

![image-20230301212340899](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012123977.png)

![image-20230301212611362](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012126405.png)

> 正片层signal：所见即所得，放铜线就能看到铜线（顶层一定是正片层）
>
> 负片层plane：一层都是铜，不能用导线，用铜的话回到正片层，只能用==放置线条==

### PCB交互式和模块化布局

> 文件栏 - 右键 - 垂直分割 - 一边原理图、一边PCB
>
> 工具 - 交叉选择模式
>
> 工具 - 器件摆放 - 在矩形区域排列

![image-20230301224210837](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012242028.png)

> 如果有器件偏移，就去PCB库更新全部
>
> 右键 - 查找相似 - 锁定元素（不需要锁定位号）

![image-20230301225016873](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012250924.png)

### PCB布局的常用命令

> 右下到左上框选：碰到的器件都被选中
>
> 左上到右下框选：全部框住的器件才选中

> 拖动器件 + L     切换器件所在层

> 选中 - 右键 - 联合

![image-20230301231916354](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012319412.png)

> 不想改动的器件 - 选中 - 锁定位置

![image-20230301232131562](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303012321639.png)



### 鼠线（飞线）

> 复制PCB到当前PCB，勾选3项

![image-20230302112529829](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021134936.png)

> 绿色DRC报错，取消布线

![image-20230302112604209](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021126283.png)

> 隐藏飞线，按N - 隐藏连接 - 网络



> 隐藏飞线 - panels - PCB - from to editor

![image-20230302114540217](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021145270.png)

> 高亮飞线

![image-20230302115322401](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021153508.png)

> 飞线不显示的原因：

![image-20230302115712339](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021157411.png)



### class类的创建和应用

![image-20230302115819355](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021158399.png)

> 设计 - 类 （进行分类设计）

![image-20230302121005549](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021210607.png)

> 设计 - 规则 - 根据类指定线宽

![image-20230302121619473](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021216549.png)



### 差分

> 两根信号线一起走线，为了抵消噪声对信号的影响

### 高效布线

> 多根线一起走

![image-20230302123308380](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021233455.png)

> 隐藏部分元素

![image-20230302125253800](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021252970.png)

![image-20230302131158515](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021311599.png)

### active route自动布线

> 打开功能

![image-20230302135136769](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021351810.png)

> 选择config

![image-20230302135222774](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021352843.png)

> 激活功能

![image-20230302142515348](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021425407.png)

> 使用功能

![image-20230302142654402](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021426534.png)

> 绘制大概路线

![image-20230302143302656](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021433738.png)

### 泪滴

> 泪滴的作用

![image-20230302143537841](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021435907.png)

> 什么是泪滴？ 一段圆弧

![image-20230302143653825](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021436876.png)

> 工具 - 泪滴

![image-20230302144419427](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021444502.png)

### 覆铜 

> 放置 - 铺铜

![image-20230302160942991](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021609030.png)

![image-20230302161115999](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021611034.png)

> 选中之后- 重新铺铜

![image-20230302161235878](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021612928.png)

> 避免死铜，避免覆铜网络和铺铜不一致

![image-20230302161619526](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021616578.png)



### cutout

> 作用

![image-20230302165339875](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021653919.png)

> 放置 - 铺铜挖孔

![image-20230302165449510](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202303021654554.png)



## 看到40集 没时间实操 开始糊涂了 需要再看