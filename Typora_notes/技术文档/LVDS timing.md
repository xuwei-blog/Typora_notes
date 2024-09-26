# LVDS时序

[TOC]







## 基于如下时序  对lvds参数进行配置

![image-20240816093528015](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202408160935113.png)



### 1. **Horizontal Timing（水平方向时序）**:
- **Horizontal Total Time (tHP)**: 
     - 表示从==一行开始到下一行开始所需的总时间==。它包括了水平的==活动时间==和水平的==消隐时间==。
     - \( total = active + HB \)
- **Horizontal Active Time (tHadr)**:
     - 也称为显示时间，指在水平方向上==实际显示图像数据的时间==。
- **Horizontal Blanking Time (HB)**:
     - 指水平方向上没有图像数据输出的时间段。这个时间段包括了水平同步信号脉宽（HSPW）和水平前后消隐时间（HSO和HW）。
     - 水平消隐时间（HB）可以表示为： \( HB = HSPW + HSO + HW \)
- **Horizontal Sync Offset (HSO)**:
     - 从一行开始到水平同步信号开始的时间。水平==前消隐时间==
     - 一般情况下，HSO通常设置得较小，以确保有足够的时间从一行结束到下一行同步信号的开始。可以==初步估计在30到50个时钟周期内==。
- **Horizontal Sync Pulse Width (HSPW)**:
     - 水平同步信号的脉冲宽度，通常是水平消隐时间的一部分。
     - HSPW一般设置得相对较大，以确保同步信号有足够的时间来稳定地传递给显示器。这个值==通常比HSO大==，==经验上设置为80个时钟周期==。
- **Horizontal Back Porch (HW)**
     - 水平后消隐时间 , 水平同步信号结束到下一行图像数据开始之间的时间。


### 2. **Vertical Timing（垂直方向时序）**:
   - **Vertical Total Time (tVP)**:
     - 表示从一帧开始到下一帧开始所需的总时间。它包括了垂直的活动时间和垂直的消隐时间。
     - \( tVP = tVadr + VB \)
   - **Vertical Active Time (tVadr)**:
     - 也称为垂直显示时间，指在垂直方向上实际显示图像数据的时间。
   - **Vertical Blanking Time (VB)**:
     - 指垂直方向上没有图像数据输出的时间段，包含了垂直同步信号脉宽和垂直前后消隐时间。
   - **Vertical Sync Offset (VSO)**:
     - 从一帧开始到垂直同步信号开始的时间。
   - **Vertical Sync Pulse Width (VSPW)**:
     - 垂直同步信号的脉冲宽度。
   - **Vertical Width (VW)**:
     - 可以理解为垂直消隐期间的宽度，垂直后消隐时间。

### 3. **参数之间的关系**:

- **像素时钟(pixels rate)**  =  ${Horizontal Total Time    \times    Vertical Total Time   \times  frame rate \over 10^6}$

   - **总周期 (Total Period)** = 活动时间 (Active Time) + 消隐时间 (Blanking Time)
   - **同步信号位置 (Sync Offset, SO)**: 消隐时间的一部分，用于确定同步信号的开始位置。
   - **同步信号脉宽 (Sync Pulse Width, SPW)**: 是同步信号的持续时间，通常位于消隐时间内。

