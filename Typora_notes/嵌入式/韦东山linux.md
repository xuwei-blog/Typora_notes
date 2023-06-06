# 韦东山Linux

## 概述

[TOC]

## linux简介

### 与windows对比

> 在linux中，树状结构表示文件夹与文件，没有盘符概念

![image-20230509013137218](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305090131625.png)

### 挂载

> sd：磁盘
>
> a：第一个磁盘
>
> 1：第一个分区
>
> 磁盘sda1 挂载 在 根目录

![image-20230509021326369](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305090213418.png)

### 文件

![image-20230509020433451](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305090204916.png)

### 命令格式

> linux命令由3部分构成：
>
> 1. command命令
> 2. options选项
> 3. parameter参数

> 中括号：不强制要求填写
>
> 尖括号：必须填写

> 注意命令和文件的区别，执行文件需要文件路径，执行命令已经提前设置好了环境变量

![image-20230509195647809](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305091956913.png)

### shell

![image-20230509200257065](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092002148.png)

### 设置环境变量

#### 临时设置

> 关闭当前终端后，设置将无效

![image-20230509203629996](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092036029.png)

#### 永久设置

1. 将程序拷贝到环境变量文件夹中

```
cp hello /usr/local/sbin
```

2. ![image-20230509203922980](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092039011.png)

3. ![image-20230509204021444](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092040479.png)

### 目录与文件操作命令

#### 相对路径

![image-20230509204748555](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092047600.png)

#### pwd

![image-20230509204819633](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092048669.png)

#### cd

![image-20230509204833600](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092048639.png)

![image-20230509205229037](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092052074.png)

#### mkdir

![image-20230509205305963](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092053012.png)

#### rmdir

![image-20230509205318500](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092053550.png)

#### rm

> -r：递归删除
>
> -f：强制删除

![image-20230509205514905](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092055960.png)

#### ls

> -a：显示隐藏文件（文件前面带.的）
>
> -l：详细显示

![image-20230509205625936](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092056991.png)

#### mv

> 改名

```
mv 1.txt 2.txt
```

> 移动

```
mv 1.txt ../
```

> 移动，改名

```
mv 1.txt ../2.txt
```

#### cat

> 显示文件内容

```
cat 1.txt
```

#### cp

> 复制一份

```
cp 1.txt 2.txt
```

#### touch

> 摸一下文件，不修改文件内容，修改文件修改时间

```
touch 1.txt
```

### 文件的权限

#### 文件属性

![image-20230509213301742](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092133790.png)

#### 修改权限

![image-20230509213539182](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092135253.png)

```
chmod 675 hello
```

> 注意：只有当权限都没有时（000），管理员也不能用，只要有人能用（700、070、007），超级管理员就能用

- 特殊操作

> 消除三者的 可执行权限

```
chmod -x hello
```

> 加上三者的 可执行权限

```
chmod +x hello
```

![image-20230509215434259](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092154322.png)

- 修改文件夹权限

> -R:递归修改文件夹内所有文件权限

![image-20230509215555936](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092155976.png)

#### 修改root密码

> 一般不用root用户，sudo 临时使用root权限比较常用

![image-20230509220206966](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092202022.png)

### 查找命令

#### 查找文件

> 可以使用通配符

![image-20230509221454820](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092214902.png)

#### 根据字符查找文件

> -r：递归查找
>
> -w：整词查找
>
> -n：显示行号

![image-20230509221335883](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092213956.png)

### 解压缩

#### gzip

> 不建议使用，因为只能处理文件，不能处理文件夹

![image-20230509223156559](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092231660.png)

#### bzip2

> 不建议使用，因为只能处理文件，不能处理文件夹

![image-20230509224012538](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092240597.png)

#### 压缩实例

> bzip2压缩比较狠，bzip2压缩率更高

![image-20230509224137886](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092241978.png)

#### tar

![image-20230509225351012](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092253089.png)

##### 压缩实例

![image-20230509224601964](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092246049.png)

![image-20230509224635095](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092246133.png)

### 网络命令

> 如果不能上网，才需要研究网络命令

> 如果电脑能上网，虚拟机配置NAT网络后，虚拟机就能上网

## VI编辑器

### 操作逻辑

> vi 文件名 [+2]
>
> 打开文件，如果没有文件就创建文件，可以添加光标默认行数的参数

![image-20230509231752279](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092317332.png)

### 基本操作

#### 命令行模式下

> 输入冒号（:）,启动命令行模式

![image-20230509232003277](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092320316.png)

#### 进入编辑模式

![image-20230509232048274](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092320339.png)

#### 一般模式

- 移动

> 补充gg：跳到第一行

![image-20230509233549578](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092335631.png)

- 处理文档

![image-20230509235209168](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092352225.png)

#### 复制/粘贴

> p，在光标之后一行粘贴

![image-20230509235500586](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092355627.png)

#### 查找/替换

![image-20230509235705213](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092357263.png)

![image-20230509235738733](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305092357799.png)

## 嵌入式开发流程

> 推荐使用linux系统编辑+编译
>
> windows和开发板 串口通信
>
> 服务器和开发板 通过NFS（也可以TFTP或者FZ）

![image-20230510000756106](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305100007181.png)

### GCC编译过程

![image-20230511110036211](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111100259.png)

![image-20230511105944389](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111059444.png)

### GCC编译内部详情

> -v：查看编译详情

![image-20230511114224542](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111142570.png)

> cc1命令：将.c转换成.s（包括预处理和编译过程）
>
> as命令  ：将.s转换成.o（汇编）
>
> collect2：将.o组装成App（链接）

### GCC常用选项

![image-20230511121703146](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111217193.png)

> -c：不链接

![image-20230511120624212](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111206287.png)

### 静态库

![image-20230511122214340](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111222385.png)

### 动态库

![image-20230511130149691](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111301732.png)

### 编译其他选项

![image-20230511125952236](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111259280.png)

### NFS

> Net File System：网络文件系统

开发板157从Ubuntu服务器的目录中拿文件

> NFS使用步骤
>
> 1. 开权限
> 2. 启动NFS服务
> 3. ubuntu服务器文件 挂载到（mount） 开发板

> 查看权限

![image-20230510153243991](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305101532481.png)

> 查看NFS服务是否开启

![image-20230510153456775](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305101534810.png)

> Ubuntu自己挂载自己

![image-20230510153930229](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305101539291.png)

### 编译设备树、内核、驱动

### buildroot编译







## makefile

#### 规则

![image-20230511145511967](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111455010.png)

> 比较时间

> a.o b.o如果比test文件新，则重新编译a.c  b.c 再重新链接

![image-20230511144907225](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111449267.png)

- 通配符

![image-20230511151101660](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111511693.png)



- 假想的目标文件（假想目标）

![image-20230511154019837](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111540868.png)

- 变量

![image-20230511155632734](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111556799.png)

#### makefile函数

> 功能

![image-20230511095828263](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305110958354.png)

> 实例

![image-20230511094602265](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305110946337.png)

> 输出如下

![image-20230511094721915](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305110947957.png)

### 通用Makefile

> 新手先会使用

![image-20230511101623247](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305111016345.png)

## 文件IO

### 驱动类型

- 字符驱动
- 块驱动

### 设备号

> 主设备号：确定哪个驱动
>
> 次设备号：确定哪个硬件

### 系统调用

> 应用程序app通过glibc触发系统异常，从而调用内核的系统调用函数
>
> swi：32位arm
>
> svc：64位arm

![image-20230524231526397](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305251534522.png)

## 应用开发

### frambuffer



### LCD操作原理

> bpp：每个像素用多少位表示颜色

![image-20230524233417388](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305251534357.png)

### 字符编码

> ANSI 如何分辨哪些是ASCII码？
>
> bit7为0：是ASCII码
>
> bit7为1：是其他编码

#### UTF16

- UTF-16 LE（小字节序，权重低的在前面）
- UTF-16 BE（大字节序）

- UTF-8

> BOM：带有头部

![](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305251534345.png)

![image-20230525153816892](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305251538967.png)

![image-20230525153612338](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305251536392.png)

### freetype

> 矢量字体



### 输入系统

