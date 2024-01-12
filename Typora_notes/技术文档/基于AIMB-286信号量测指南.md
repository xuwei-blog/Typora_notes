# 基于AIMB-286信号量测指南

[TOC]



> 内容从以下三个方面展开：
>
> - 基础常识篇
> - 全流程量测信号篇
> - 细节整理





## 基础常识篇



## 信号量测篇



## 细节整理

1. 主板号以==芯片组型号==来命名，286为300系主板

    ![image-20240111114519562](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401111145453.png)

    芯片组的系列级别：

    - H系列
    - B系列
    - Z系列
    - X系列

    

2. CPU型号的认识

    | CPU系列                 |      |      |
    | ----------------------- | ---- | ---- |
    | CORE          酷睿系列  |      |      |
    | PENTIUM   奔腾系列      |      |      |
    | CELERON   赛扬系列      |      |      |
    | Xeon           至强系列 |      |      |

    ![img](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401111149073.jpg)

3. CPU型号与阵脚关系

    |  CPU代数  |           CPU引脚           | 芯片组    |
    | :-------: | :-------------------------: | --------- |
    |   2/3代   |           LGA1155           | H6X/7X    |
    |   4/5代   |           LGA1150           | H8X/9X    |
    |   6/7代   |           LGA1151           | H100/H200 |
    |   8/9代   |           LGA1151           | 300       |
    |  10/11代  |           LGA1200           | H400/H500 |
    |  12/13代  |           LGA1700           | H600/700  |
    | 服务器CPU | LGA2011  LGA2011-3  LGA2066 |           |

    

4. 芯片组的封装BAG (球栅阵列封装)

    ![img](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401111350085.jpg)

5.  IO的厂家，封装 QFP（四边又脚向外延申）

    - NUVOTON 新唐，曾叫华邦

        ![img](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401111359152.png)

    - Fintek 精拓

        ![img](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401111400595.jpg)

    - ITE 联阳

        ![img](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401111400433.png)

    - Winbond 华邦

        ![img](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401111401949.jpg)

    - SMSC 史恩斯

        ![img](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401111401082.jpg)

        

6.  IO作用

    - 管理触发上电/检测
    - 管理KB/ME（PS2）
    - 管理COM口（COM芯片75232/75185，通讯标准RS232）
    - 管理LPT（针式打印机）
    - 管理软驱FDD

7. BIOS封装形式

    - SOP 两边有脚向外延展
    - DOP 双列直插

8. 1

9. 2

10. 21

11. CPU核心供电

    - 集显供电在内存供电之后产生

12. 123

13. 