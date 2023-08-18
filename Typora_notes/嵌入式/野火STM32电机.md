# 野火STM32电机

## 概述

[TOC]

## 电机简介

### 直流电机

> 直流有刷：电刷、换向器，电刷和换向器接触从而驱动电机
>
> 直流无刷：转子、定子

![image-20230610160838618](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101608727.png)

#### 特点

![image-20230610161123001](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101611062.png)

#### 电机驱动器

> 直流有刷电机：需要一个全桥（H桥），对角线接通Vcc、GND后，驱动电机
>
> 直流无刷电机：需要3个半桥

> H桥左半边，2个mos管，形成推挽电路，2个推挽电路形成H桥，3个形成三相无刷
>
> mos管控制极高电平导通，低电平断开
>
> 上边导通下边断开则输出高电平
>
> 上边断开下边导通则输出低电平
>
> 两边都断开，输出高阻态
>
> 两边都导通，电源短路

![image-20230610161650566](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101616617.png)

### 步进电机

![image-20230610162009457](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101620509.png)

#### 构造

![image-20230610162205035](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101622090.png)

> AB两相

![image-20230610162329135](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101623188.png)

#### 外观尺寸

![image-20230610162449344](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101624401.png)

### 伺服电机

> 一般来说，伺服电机指：伺服电机控制系统+伺服电机，MCU只需要对控制器
>
> 进行控制，控制器再对伺服电机进行调整，这是一个闭环系统

> 停止对直流电机控制信号，直流电机会因为惯性继续运动
>
> 然而伺服电机信号电压为0，不会运动

> 伺服电机转矩随着转速的增加而匀速下降

![image-20230610162711457](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101627501.png)

#### 特性

![image-20230610163226802](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101632850.png)

### 舵机

![image-20230610163322086](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101633134.png)

#### 舵机的分类

<img src="https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202306101634810.png" alt="image-20230610163459750" style="zoom:33%;" />

