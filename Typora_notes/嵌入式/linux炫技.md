# linux高端操作合集

[TOC]

> 诞生于1996，梦想做说唱领袖



## 任务调度cron

### 安装

```
apt-get install cron
```

### 流程

> 以每隔一分钟将日期打印到文本为例
>
> 1. 编写  .sh 脚本
>
>     ```shell
>     date >> ./date_test.txt
>     ```
>
> 2. 将 .sh 设置为可执行
>
>     ```
>     chmod 744 test.sh
>     ```
>
> 3. 启动任务调度
>
>     ```
>     crontab -e
>     ```
>
> 4. 此时可以看到现象
>
> 5. 关闭任务调度
>
>     ```
>     crontab -r
>     ```

### CRON表达式

```
例子：
    # 每月的最后1天
    0 0 L * * *

    说明：
    Linux
    *    *    *    *    *
    -    -    -    -    -
    |    |    |    |    |
    |    |    |    |    +----- day of week (0 - 7) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
    |    |    |    +---------- month (1 - 12) OR jan,feb,mar,apr ...
    |    |    +--------------- day of month (1 - 31)
    |    +-------------------- hour (0 - 23)
    +------------------------- minute (0 - 59)
```

#### CRON表达式

| 字段(默认5位) | 是否必填 | 允许值          | 允许特殊字符            | 备注                                                         |
| :------------ | :------- | :-------------- | :---------------------- | :----------------------------------------------------------- |
| Seconds       | 否       | 0–59            | ``*`` ``,`` ``-``       | 标准实现不支持此字段。                                       |
| Minutes       | 是       | 0–59            | ``*`` ``,`` `-`         |                                                              |
| Hours         | 是       | 0–23            | ``*`` `,` `-`           |                                                              |
| Day of month  | 是       | 1–31            | `*` `,` `-` `?` `L` `W` | `?` `L` `W`只有部分软件实现了                                |
| Month         | 是       | 1–12 or JAN–DEC | `*` `,` `-`             |                                                              |
| Day of week   | 是       | 0–7 or SUN–SAT  | `*` `,` `-` `?` `L` `#` | `?` `L` `#`只有部分软件实现了 Linux和Spring的允许值为0-7，0和7为周日 Quartz的允许值为1-7，1为周日 |
| Year          | 否       | 1970–2099       | `*` `,` `-`             | 标准实现不支持此字段。                                       |

> 通配符

| 符号 | 作用 | 示例                                                         |
| ---- | ---- | ------------------------------------------------------------ |
| *    | 每一 | * * * * * ：每分钟执行一次                                   |
| ，   | 并列 | * 2,4 * * * ：每天的2点和4点                                 |
| -    | 连续 | 20-40 * * * * : 每小时的第20到40秒，每小时执行21次（闭区间）一天共执行21 X 24次 |
| /    | 整除 | */2 * * * * ：分钟字段可以被2整除的，都会被执行一次，等价于 2,4,6,8... * * * * |

> 注意事项：
>
> 1. 月份字段、星期字段，为了避免歧义，可以使用英文缩写
>
> 2. 星期可以指定W（工作日），日和星期可以指定L（最后一天）
>
> 3. 混淆点 ，1和2等价，等价于0、2、4、6...，3等价于1、3、5、7... ， 若7/2 ，则等价于7、9、11...
>
>    - */2
>    - 0/2
>    - 1/2
>
> 4. 只有5位，如何表示秒
>
>    ```
>    1. 先指定* * * * * ,每分钟执行一次
>    2. 再添加shell指令，sleep(1)
>    3. 再指定* * * * * ,每分钟执行一次
>    4. 直到添加第59个sleep(1)
>    5. 这个逻辑应该可以用循环后续再学
>    ```

> 参考案例

在每周五、周日的17点执行一次脚本

```
0 17 * * sun,fri /scripts/script.sh
```

每4个小时执行一次脚本

```
0 */4 * * * /scripts/script.sh
0 0/4 * * * /scripts/script.sh
```

每年执行一次任务

```text
@yearly /scripts/script.sh
```

系统重启时执行

```text
@reboot /scripts/script.sh
```



### 常用命令

```
crontab -r	#终止任务调度
crontab -l	#列出当前的任务调度
crontab -e	#编辑任务调度
service cornd restart #重启任务调度
```



### 常见问题

> 1. 部分脚本无法执行， 但是  ./test.sh 可以执行
>
>     原因：无法读取环境变量
>
>     - 解决方法
>
>         - 写成绝对路径
>
>         - shell脚本开头使用以下代码
>
>             ```shell
>             #!/bin/sh
>              
>             . /etc/profile
>             . ~/.bash_profile
>             ```
>
>         - 在 /etc/crontab 中添加环境变量，在可执行命令之前添加命令 . /etc/profile;/bin/sh，使得环境变量生效
>
>             ```
>             20 03 * * * . /etc/profile;/bin/sh /pwd/test.sh
>             ```
>
>             
>
> 2. 备份cron，还原cron
>
>     ```
>     # crontab -l > cron-backup.txt
>     # crontab -r
>     # crontab -l         ==》   no crontab for root
>     # crontab cron-backup.txt
>     ```



## find & grep

| 命令 | 基本语法              | 作用   |
| ---- | --------------------- | ------ |
| find | find   .   -name  “a" | 找文件 |
| grep |                       | 找内容 |

### find

> 基础语法

```shell
find 目录 -测试表达式
```

> find后面所有内容都可以省略，默认有pirnt动作(换行显示)

```shell
find ./ -name a.jpg -print
```

```shell
find . a.jgp
```



| type可选值 | 表示     |
| ---------- | -------- |
| f          | 普通文件 |
| d          | 目录     |
| l          | 软链接   |
| s          | 套接字   |
| b          | 块设备   |
| c          | 字符设备 |
| p          | 管道     |

#### 常用案例

> 案例

```shell
# 精确查找，完全匹配，当前目录下的所有a.txt文件
find ./ -name a.txt -print
find . -name a.txt
# 查找当前目录下的a，但不确定是目录还是文件
find . -name a -print -ls
# 确定要查找的是目录,默认是逻辑与 -and
find . -name a -a -type d -print -ls
find . -name a -type d -print -ls
# 使用通配符时，要加引号 " "
find . -name "*abc*" -a -type d -print -ls
# 查找当前目录下，名称是a，并且不是目录
find . -name a -not -type d -print
find . -name a ! -type d -print
# 查找a，或者a.jpg,使用默认动作 -print
find ./ -name a -o -name a.jpg
# 查找a，或者a.jpg,不使用默认动作 -print ，打印内容有区别
find ./ -name a -o -name a.jpg -ls   
# 应该使用强制优先，()前面需要转义符，并且()需要有空格
find ./ \( -name a -o -name a.jpg \) -ls   
# 不区分大小写 -iname ，查找a
find ./ -iname a
# 查找空目录
find . -empty -type d -ls
# 控制输出格式,仅文件名
find . -name a -printf "%f\n"
# 控制输出格式,仅文件路径
find . -name a -printf "%h\n"
# 控制输出格式,仅搜索路径以外的内容
find $(pwd) -name a -printf "%P\n"
# 精确查找，当前目录下的所有a文件，输出到文件b中，没有b则创建，有则覆盖
find . -name a -fls /tmp/b
# 以上类似于
find . -name a -fprint /tmp/b
# 查找当前目录下a，排除`pwd`/ba 子目录 ,使用命令替换必须用引号
find `pwd` ! -path "`pwd`/ba/*" -name a
find `pwd` -name a ! -path "`pwd`/ba/*"
# 查找深度为1 ，maxdepth全局选项，要求在 指定位置后，测试表达式之前
find `pwd` -maxdepth 1 -name "[0-9].jpg"
# 如果只想搜索2级目录
find `pwd` -maxdepth 2 -mindepth 2 -name "[0-9].jpg"
```



## 定时任务at

> 基本介绍
>
> - at命令是一次性定时计划任务，at的守护进程atd会以后台模式运行，检查作业队列来运行
> - 默认情况下，atd守护进程每60秒检查作业队列，有作业时，会检查作业运行时间，如果时间与当前时间匹配，则运行此作业
> - at时一次性定时计划任务，只执行一次
> - at命令使用前，要保证atd进程的启动

![image-20240313103405084](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202403131034141.png)

> 检查atd守护进程有没有启动，本条命令也有相关进程

```shell
ps -ef | grep atd
```

> 相关指令

| 指令 | 作用                                                         |
| ---- | ------------------------------------------------------------ |
| atq  | 查询任务队列，q：quest，探求                                 |
| at   | 设置定时时间，进入后    ctrl+（space  、 del），ctrl+d ：结束at命令的输入 |
| atrm | 删除编号为6的定时任务，atrm 6                                |
|      |                                                              |
|      |                                                              |

![image-20240313103934745](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202403131039802.png)



![image-20240313104048970](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202403131040101.png)

### at案例

![image-20240313104154265](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202403131041364.png)

## 分区

### 前置知识

> 分区的两种方式
>
> - MBR分区
>     - 最多支持4个主分区
>     - 系统只能安装在主分区
>     - 扩展分区要占一个主分区
>     - MBR最大只支持2TB，兼容性很好
> - GPT分区
>     - 支持无限个分区，但受OS限制，windows下最多128个分区
>     - 最大支持18EB容量（EB = 1024PB , PB = 1024 TB）
>     - windows7 64位之后支持GPT



### 分区结构图

![image-20240222160747642](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402221607012.png)

> linux下的硬盘
>
> 1. linux下的硬盘分为 IDE 硬盘 和 SCSI 硬盘 ，目前基本上是 SCSI硬盘
>
> 2. IDE硬盘，驱动器标识符为  `hdx~` ，其中 `hd` 表明是IDE硬盘 ，`x`为盘号，`~` 代表分区
>
>     ```
>     # x 的4种情况
>     a为基本盘
>     b为基本从属盘
>     c为辅助主盘
>     d为辅助从属盘
>     
>     # ~ 的几种情况
>     前4个分区用数字1到4表示，他们是主分区或扩展分区，从5开始就是逻辑分区
>     ```
>
>     ```
>     # 案例
>     hda3		# 表示第一个IDE硬盘上的第三个主分区或者扩展分区
>     ```
>
> 3. SCSI硬盘 与 IDE硬盘类似，标识符为 `sdx~`  ，其中 `sd` 表明是SCSI硬盘

 

### 添加一块硬盘

> 流程：
>
> 1. 连接一块硬盘
>
>     ```
>     lsblk -f		# 查看硬盘分区情况，需要重启才能看到硬盘
>     reboot
>     ```
>
>     ![image-20240222171045416](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402221710506.png)
>
> 2. 分区
>
>     ```
>     fdisk /dev/sdb	# 输入m进入帮助
>     root@user# n	# 添加一个新分区
>     root@user# p	# 将硬盘设为1个主分区
>     root@user# w	# 将设置写入硬盘
>
>     # 操作完成后没有文件系统，没有uuid号，没有挂载路径 ，因为分区还没初始化
>     ```
>
> 3. 格式化
>
>     将sdb1格式化成如下配置
>
>     ```
>     mkfs -t ext4 /dev/sdb1
>     ```
>
> 4. 挂载
>
>     ```
>     mkdir /home/newdisk
>     mount /dev/sdb1 /home/newdisk	# 这是临时挂载
>     
>     # 如何取消挂载呢
>     umount /dev/sdb1 或者 /home/newdisk
>     ```
>
> 5. 设置永久挂载
>
>     ```
>     vim /etc/fstab
>                                 
>     # 编辑完之后
>     mount -a 	# 自动挂载，使得永久挂载的设置生效
>     ```
>
> ![image-20240222172758288](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402221727363.png)



### 磁盘指令

- 磁盘情况查询

```
df -lh
```

| 参数 | 功能                                        |
| ---- | ------------------------------------------- |
| -a   | –all,显示全部文件系统列表                   |
| -h   | 方便阅读的形式来显示结果                    |
| -B   | 指定分区块大小                              |
| -l   | 只显示本地文件系统                          |
| -i   | –inodes 列出 inode 资讯，不列出已使用 block |
| -T   | 显示系统文件类型                            |
| -P   | 输出格式为POSIX                             |



- 查询指定目录的磁盘占用情况

```
du -h /dir
```

| 参数          | 功能                       |
| ------------- | -------------------------- |
| -s            | 指定目录占用大小汇总       |
| -h            | 带计量代为                 |
| -a            | 含文件                     |
| --max-depth=1 | 子目录深度                 |
| -c            | 列出明细的同时，增加汇总值 |



#### 案例

1. 统计文件个数

    > 以 `-` 开头的不是目录文件
    >
    > 先列出来，再过滤(正则表达式)，再统计

    ```
    ls -l /home | grep "^-" | wc -l
    ```

    

2. 统计文件夹下文件的个数，包括子目录下的文件

    ```
    ls -lR /home | grep "^-" | wc -l
    ```

3. 树状显示目录结构

    ```
    apt-get install tree
    tree	# 从当前目录开始，展示所有内容
    ```

    



## 网络

> 电脑中的硬件涉及到的两种地址
>
> - IP地址
>     - 逻辑地址，不唯一
> - MAC地址
>     - 硬件地址，全球唯一，不能更改，仿冒MAC地址除外

### NAT

> 一些整理的知识：
>
> 1. 虚拟机可以将vmnet8虚拟网卡的IP 设为其他网段
> 2. 

![image-20240223100334477](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402231003572.png)

> 如何修改虚拟机网段 和 查看 网关

![image-20240223132129471](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402231321582.png)



### 主机号和hosts映射

> 黑客篡改hosts映射，实现DNS劫持，将网站映射到盗号IP页面

> linux，hosts目录位置 /etc/hosts
>
> windows，hosts目录位置 C：windows  \ system32 \ drivers \ etc \ hosts

### IP地址和子网掩码

> 用于判断IP地址的网络号和主机号。
>
> 网络号用于标识某个主机属于哪个网络，主机号用于判断某台主机
>
> 比如192.168.6.123 / 255.255.255.0 （24）这台主机，网络号为192.168.6.0，主机号为192.168.6.123



### ping的各种意义

> 127.0.0.1 是本地循环地址，如果本地址无法Ping通，则表明本地机TCP/IP协议不能正常工作

```
ping 127.0.0.1
```

> ping本机的IP地址，用IPConfig查看本机IP，然后Ping该IP，通则表明网络适配器（网卡或MODEM）工作正常，不通则是网络适配器出现故障



## 进程管理

> LINUX中，每一个执行的 `程序` 被称为一个进程，会分配一个ID号（PID）
>
> 每个进程以两种方式存在，前台 和 后台







