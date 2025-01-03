# LVDS通关手册

## 概述

[TOC]

作者：ASH-FAE 徐威 

版本：v1.0

手册目的：逐步指导LVDS的学习，每一个小步骤前后都有注意事项，步骤后的notes操作完毕再看，如果操作进行不下去再配合操作后的notes配合理解。

## 第一阶段 硬件

### 接线

1. 工具材料准备

> notes：
>
> - 同时打开==主板引脚定义== 和 ==显示屏引脚定义==，找到pin1的位置
> - 数一下有几根数据线、接地线、控制信号线，这3类线==分批接线==，每批线接完都要检查
> - 正式接线前，最好==在心中接一遍线==，尽量不要拆线

![需要的工具](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231955643.jpg)



2. 如何插线

> notes：
>
> - ==接头==有两面，张开双臂的那一面朝模具里，有个小突出的那一面朝外
> - 观察模具，有个==小三角==的位置为pin1，在pin1那一侧，有pin5，pin15，pin25...的记号
> - 偶数pin引脚的一侧，有pin10，pin20，pin30...的记号，==方便定位==
> - 所有线都插完后，把==模具上的小扣子==挨个按一下，多余的线缠绕起来，然后准备用万用表测试
>

![如何插线](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412232000115.jpg)

> notes：
>
> - 接头的小突出是挂在模具外壳上的，能看见银色反光说明插紧了
> - 接头上的两个手臂，是用来插主板上针脚的，如果双臂太宽，容易接触不良





3. 如何拔线

> notes：
>
> - 镊子放在如图所示==小扣子==的位置，==控制力度==将塑料片==略微翘起==
> - 一边翘起，一边控制力度拔线

![如何拔线](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231955580.jpg)

> notes：
>
> - 要控制镊子挑的力度，用力过猛这个引脚接口就==报废==了





4. 如何缠线

> notes：
>
> - 每根线单独缠一圈

![如何缠线](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231955388.jpg)



### 硬件验证

1. 用接口将显示屏和主板连接

> notes：
>
> - 只需要将显示屏和主板连接，暂时==不要通电==
> - 再次检查pin1的位置，必须正确
> - 一共连两根线，一根lvds，一根背光

![硬件连接](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231955175.jpg)

> notes：
>
> - 显示屏和主板连接的目的是：让==硬件有回路==，方便测试是否接地



2. 使用万用表验证供电

> notes：
>
> - 目的：供电引脚==不能碰到==接地信号，必须==避免电源短路==，一旦触碰，上电后显示屏报废
> - 将万用表调到如图==蜂鸣器档位==，测得短路则会报警，两表笔触碰有警报后继续操作
> - 主板上所有裸露的金属外壳都接地，黑表笔接地，红表笔测供电引脚，要求不能有警报
> - 背光供电，lvds显示供电，都要验证

![万用表](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231956930.jpg)



![接地](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231956443.jpg)

3. 使用万用表验证接地线

> notes：
>
> - 对照之前数到的接地信号个数，验证是否有同等个数的警报声



4. 最后验证

> notes：
>
> - 线序检查
> - 主板跳线帽检查
> - 供电、接地专项检查





### 上电测试

1. 修改主板BIOS

> notes：
>
> - 给主板接一个可以正常显示的屏，并且给主板安装好系统、官网驱动
> - 设置BIOS，启动LVDS并选择分辨率

![73576a8f1adfb494d40747c5427ae15](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231956913.jpg)

**调BIOS步骤**

![142e9f15c36f03fd45c8c5bb095d020](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231956510.jpg)

![99d1d3430e4a992217c0051c91f0fa7](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231956411.jpg)

![8c53be549e73562e37de155b17cedfc](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231956952.jpg)

![97b973b363721f1f648753e4ce43a9a](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231956295.jpg)

> notes：
>
> - VBIOS上的分辨率一共有16种，如果从0开始标号，标号为0~15





2. 给主板供电

> notes：
>
> - 观察是否有背光，是否有显示，有背光无显示说明线序有问题，无背光无显示说明主板没有获得det信号





3. 用万用表测试显示屏供电电压和背光供电电压

> notes：
>
> - 将万用表调到如图档位，黑表笔接地，红表笔测供电、使能信号，判断是否达到显示屏的供电要求
> - 主板通电的过程中，表笔==不要随意测量==，避免表笔探针将两引脚短路
> - 如果lvds显示和背光都没有供电，背光使能处于无效状态，则进行线序测试

![40c824705c1902b0630314e5b07e272](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957657.jpg)

> notes：
>





4. 线序测试

> notes：
>
> - 目的：给主板一个det信号，让主板进行供电
> - 将如图接口插入主板，上电测试lvds显示供电 和 背光供电，如果有供电，则表明之前lvds线序有问题，如果没有供电，则表明det信号有问题

![f6d089ebac8eb99fca75fc22b87d4e8](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957571.jpg)

> notes：
>
> - ​		如果还没有点亮屏幕，可能会有以下几个情况：
>
>     1.主板BIOS未设置LVDS
>
>     2.线材有问题，可以通过万用表测量
>
>     3.接口一直插拔有松动，导致接触不良，可以拔掉部分信号线排查接触不良的信号
>
>     4.未设置跳线帽，驱动电压不够
>
>     

## 第二阶段 软件

### LVDS基础

#### 屏幕如何显示

> notes：
>
> - 水平蓝色实线是 电子枪 扫描一行像素的路径
> - 蓝色虚线是 电子枪 回到下一行开头的路径
> - 黄色虚线是 一场画面扫描结束后 电子枪回到第一行

![显示屏](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957606.jpg)

> notes：
>
> - 随便写点东西，也许对显示屏显示有更好的理解
> - 电子枪走完一圈，则为1个场，同一时刻，可能存在多个电子枪同时扫描行
> - 1帧画面假设有2个场，第2和第3场如果画面差异较大，会明显看到画面模糊，所以需要高刷，减少每场差异
>
> - 隔行扫描interlace，又称交错扫描，行间可能看到有闪烁、细纹，去交错Deinterlaced模式可以改善画质
>
> - 逐行扫描progressive，缺点是扫描到一场结束，最初的内容可能已经淡化了，能看到显示屏上下画质差异
>
> - 扫描方式有没有可能是垂直方向的呢？这个问题可能会导致屏幕故障后是显示==竖条纹或者横条纹==
>
>     ![垂直扫描](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957717.jpg)



#### 显示屏参数

> notes：
>
> - 黄色区域，为可视区域，相当于把一幅画按比例裁剪成1280*1024的画面
> - 绿色区域，现实中为屏幕上的黑边，该区域电子枪也会扫描到

![显示屏参数](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957410.jpg)

**为了方便做记号，逻辑上将黄色可视区域缩小**

> notes：
>
> - 不同规格书上的记号可能叫法不一样，但定义一定相同，需要自行判断
>
> - ​        记号的含义
>
>     ①：Horizontal Active
>
>     ②：Vertical Active
>
>     ③：Horizontal Period
>
>     ④：Vertical Period
>
> - 3根同方向的虚线为 Horizontal Blanking，简称HB
>
> - 右下到左上的虚线为 Vertical Blanking，简称VB

![绿色](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957285.jpg)

> notes：
>
> - HB中包含3个信号，水平前浪HFP，水平后浪HBP，水平同步Hsync，单位是周期T~h~，表示一行的周期
> - VB中包含3个信号，垂直前浪VFP，垂直后浪VBP，垂直同步Hsync，单位是周期T~clk~，表示一个时钟周期





VESA**标准**



> notes：
>
> - LVDS有两种颜色格式，VESA 和 JEIDA，唯一区别就是在其中一个通道(Y3)上传输内容不一致
>
>     VESA:在Y3上传输各种颜色的==高两位==，==常用选项==
>
>     JEIDA:在Y3上传输各种颜色的==低两位==
>
> - 从VESA标准中，看出==两次可视画面之间==的信号为  前浪-同步信号-后浪

![image-20230719113430965](C:\Users\xu.wei\AppData\Roaming\Typora\typora-user-images\image-20230719113430965.png)

### 配置CH7511

1. 打开文件夹

> notes：
>
> - 创建一个专门存放LVDS的目录，将工具、数据整理好

![文件夹介绍](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957387.png)





2. 开始配置7511

> notes：
>
> - 没有提到的功能，暂时可以全部默认

![步骤2](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957497.png)

![步骤3](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957759.png)

> notes：
>
> - 选择6bit单/双通道 或 8bit单/双通道
> - 物理尺寸含显示器边框

![步骤5](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957983.png)

> notes：
>
> - ⑥ 像素时钟，会遇到的叫法：pixel clock ， clock frequency   ...
>
>     ​     可视区域尺寸，会遇到的叫法：active area 
>
> - ⑦horizontal /vertical active
>
>     ​    horizontal /vertical period
>
> - ⑧一般默认HM为0 
>
> - ⑨设置交错模式
>
> - ⑩选择数字同步信号
>
> - ⑪数字差分信号
>
> - ⑫选择水平同步和垂直同步有效方式

![步骤13](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957692.png)

> notes：
>
> - HSPW 是 Hsync这个概念的计量单位
> - HB = Hsync Period - Hsync Active  = Horizontal front porch + Horizontal back porch + HSPW
> - HSO = Horizontal front porch + HM ，一般情况 HM = 0
> - 回头去看VESA标准，在VESA标准下，HM是包含在ative内的，没有特殊说明HM为0
> - 垂直方向同理



![步骤15](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231957471.png)



![步骤16](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958272.png)



![步骤18](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958433.png)



![步骤21](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958169.png)



![步骤22](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958834.png)





![步骤23](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958512.png)



![步骤24](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958762.png)





![步骤25](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958445.png)



![步骤26](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958327.png)





![步骤27](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412231958076.png)



#### 时序图分析

> notes：
>
> - 如果前面参数我没解释清楚，可以参考以下内容(正确性需自行验证)
>
> - 如图时序图上半部分为场同步时序，下半部分为行同步时序
>
> - T~h~如果在网上搜得到的是毫英寸的单位，其实这是周期T的单位，下标是horizon，T~clk~是时钟周期
>
> - 很多情况下，HB中3个具体参数都不会给出，需要自己算
>
> - ​        首先，弄明白单位T~h~，T~clk~具体为多少，一般就看典型值Typ
>
>     由下表看出，时钟周期Tclk = 18.52ns ， 时钟频率Freq = $\frac{1}{54MHz} $ = 18.5185ns
>
>     一帧画面用时 t = $\frac{1}{60Hz} $ = 16.67ms ，扫描一行用时T~h~ = $\frac{t}{1024line} $  = $\frac{16.67}{1024} $  = 16.2793ns ，此处未考虑电子枪个数
>     
>     但是一般T~h~ 和 T~clk~ 不会使用具体数值，计量方式为几个周期
>     
> - 如下图①中， 1 个 HSPW  = T~h~，；②中， PWVS  = 2 HSPW = 2 T~h~；③中，1个clk周期为T~clk~  ；
>
>     ④中，PWHS =  T~clk~   =  T~h~；⑤中，TFPH = 3 T~clk~   ，由此再借助HB = HBP + HFP + HSPW
>
> - 综上 HB = 204 = 3 + 1 + T~水平后浪~  ， 水平后浪为 200 
>
>     ​        VB = 42 = 2 + T~垂直前浪~ + T~垂直后浪~ ， 假设T~垂直前浪~ 为 2 T~h~ ， T~垂直后浪~ = 38

![时序参数](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412232000177.png)

![时序图分析](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412232000613.png)



### 更新7511

1. 安装驱动

> notes：
>
> - 安装AUX的驱动

![驱动](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412232001538.png)



2. 准备工作

![准备工作](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412232001070.png)

3. 刷固件

> notes:
>
> - 需要将参数打包给Udp7511v1.3，才能刷入固件，直接打开Udp7511没有作用

![步骤1](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412232001477.png)

![步骤4](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202412232001042.png)





4. 重启

