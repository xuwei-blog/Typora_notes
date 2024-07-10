# 手写OS

[TOC]

> 参考资料：[从零开发操作系统_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV18K411w7Z2/?spm_id_from=333.337.search-card.all.click)
>
> [操作系统——初识MBR（一） - hawkJW - 博客园 (cnblogs.com)](https://www.cnblogs.com/hawkJW/p/13621887.html)



##框架

- 开机启动流程（输出版）

> 当电脑按下开机键，电脑以实模式的寻址方式执行，计算机执行的第一条指令，跳转到BIOS程序，BIOS初始化硬件、检查外设
>
> 之后BIOS会校验启动盘位于0盘0道1扇区的内容，若扇区末尾是55aa，说明该扇区有可执行程序MBR，加载到0x07C00并执行



- 实模式：物理地址20位，2的20次方 = 1MB

  

- 实模式1MB内存布局

| 起始地址 | 结束地址 | 大小    | 用途                                                        |
| -------- | -------- | ------- | ----------------------------------------------------------- |
| FFFF0    | FFFFF    | 16B     | BIOS入口地址，空间太小了，只能放跳转指令  jmp 0xf000:0xe05b |
| F0000    | FFFFF    | 64KB    | BIOS代码，包括上面介绍的BIOS入口地址                        |
| C8000    | EFFFF    | 160KB   | 映射硬件适配器的ROM或者内存映射式I/O                        |
| C0000    | C7FFFF   | 32KB    | 显示适配器BIOS                                              |
| B8000    | BFFFF    | 32KB    | 用于文本模式显示适配器                                      |
| B0000    | B7FFF    | 32KB    | 用于黑白显示适配器                                          |
| A0000    | AFFFF    | 64KB    | 用于彩色显示适配器                                          |
| 9FC00    | 9FFFF    | 1KB     | EBDA（Extended BIOS Data Area）拓展BIOS数据区               |
| 07E00    | 9FBFF    | 622080B | 可用区域                                                    |
| 07C00    | 07DFF    | 512B    | MBR被BIOS加载到此处，jmp 0x0:0x7C00                         |
| 00500    | 07BFF    | 30464B  | 可用区域                                                    |
| 00400    | 004FF    | 256B    | BIOS Data Area（BIOS数据区）                                |
| 00000    | 003FF    | 1KB     | Interrupt Vector Table（中断向量表）                        |



- 第一条跳转指令的解析

> jmp 0xf000:0xe05b
>
> 段基址 X 16 +  段内偏移量 e05b  = 0x fe05b 



- 如何引导OS

> 完成硬件初始化后，BIOS最后会校验启动盘位于 0盘0道1扇区 的内容，
>
> 若该扇区末尾的两个字节分别是0x55、0xaa ，则将该扇区内容加载到0x07C00处，然后跳转至该地址并执行
>
> 55aa是一个标记，用来标记该磁盘中存在可执行程序（实际上就是MBR，Master Boot Record程序）







