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

![image-20230510000756106](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202305100007181.png)