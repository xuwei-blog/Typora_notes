# linux下安装burnin

[TOC]

> 系统环境：ubuntu 20.04
>
> Eiot FAE 徐威



## 一、换源

### 1. 用vi打开镜像源文件

```shell
# 用vi打开镜像源文件
sudo vi /etc/apt/sources.list
```



### 2. 删除原先的镜像源内容

```SHELL
# 从光标所在行开始 , 删除到末行 ,  d + （shift + g）
dG
```



### 3. 将清华源地址粘贴进文件

```shell
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb http://archive.ubuntu.com/ubuntu/ trusty main universe restricted multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
# deb-src http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu focal stable
# deb-src [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu focal stable

```



### 4. 保存并退出

```shell
# vi命令
:wq
```





## 二、burnin环境配置

### 1. 没有配置好相关的库时，运行burnin，会产生报错

```shell
# 运行burnin
sudo ./burnintest.sh
```

> 缺少Qt5的库

![image-20240228141025967](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281410070.png)

### 2. 安装gcc

```shell
# 判断gcc是否安装
gcc -v
```

![image-20240228141409630](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281414680.png)

> 没有gcc则安装

```shell
sudo apt install gcc
```



### 3. 安装g++

```shell
# 判断g++是否安装
g++ -v
```

![image-20240228141550827](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281415878.png)

> 没有g++则安装

```shell
sudo apt install g++
```



### 4. 安装clang

```shell
# 判断clang是否安装
clang  -v
```

![image-20240228141840226](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281418305.png)

> 没有clang则安装

```shell
sudo apt install clang
```



### 5. 安装clang++

```shell
# 判断clang++是否安装
clang++ -v
```

![image-20240228142025763](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281420801.png)

> 没有clang++则安装

```shell
sudo apt install clang++ 
```



### 6. 安装make

```shell
# 判断make是否安装
make -v
```

![image-20240228142129977](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281421027.png)

> 没有make则安装

```shell
sudo apt install make
```



### 7. 安装make-guile

```shell
# 安装make-guile
sudo apt install make-guile
```

![image-20240228142336715](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281423762.png)



### 8. 安装cmake

```shell
# 安装cmake
sudo snap install cmake --classic
```

![image-20240228142437382](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281424451.png)



## 三、安装Qt5

### 1. 安装Qt5的组件

```shell
# 安装Qt5的组件
sudo apt-get install build-essential
```

![image-20240228142708310](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281427344.png)



### 2. 安装Qt开发工具

```shell
# 安装Qt开发工具
sudo apt-get install qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools
```

![image-20240228142800060](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281428116.png)



### 3. 安装qtcreator

```shell
# 安装qtcreator
sudo apt-get install qtcreator
```

![image-20240228143236627](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281432683.png)



### 4. 安装Qt5

```shell
# 安装Qt5
sudo apt-get install qt5*
```

![image-20240228143127963](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281431004.png)



### 5. 安装完毕，可以运行burnintest了

```shell
# 运行burnintest
sudo ./burnintest.sh
```

![f4e0c4200fd2754996b395c3a8343d5](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402281430361.png)