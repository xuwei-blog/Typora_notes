# docker

[TOC]



## 概述

1.  搬家  ==》 搬楼

2.  容器和虚拟机

    - 传统虚拟机：在硬件层面进行虚拟化
    - docker虚拟机：在OS上进行虚拟化，复用本机的OS

3. docker基本组成

    - 镜像
    - 容器
    - 仓库

4. docker（管理引擎）和docker hub （容器仓库）

    国内仓库有：阿里云；网易云

5. docker工作原理

    ![image-20240130135441106](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401301354371.png)

6. 12

## docker命令

### 启动类命令

![image-20240131095401201](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401310954297.png)

### 镜像命令

- 列出本地主机上的镜像
    - -a：列出本地所有的镜像（含历史镜像）
    - -q：只显示镜像ID

```
docker images
```

- 在云端搜索镜像
    - --limit：列出有限的镜像 （docker search --limit 5 hello-world）

```
docker search [镜像名字]
```

- 拉取镜像

```
docker pull 镜像名字[:TAG]
```

- 查看镜像/容器/数据卷所占空间

```
docker system df
```

- 删除镜像
    - -f：强制删除正在执行的容器（docker rmi -f  [images ID]）

```
docker rmi [images ID]
docker rmi [images1 ID][:TAG] [images2 ID][:TAG]
docker rmi -f $(docker images -qa)  #透传
```

> 面试题：虚悬镜像，镜像名和TAG都为NONE

### 容器命令

#### 交互窗口

- 交互模式启动镜像
    - -i：交互式操作
    - -t：终端
    - /bin/bash：提供交互式shell
    - exit：退出终端，容器会停止
    - ctrl+p+q：退出容器，容器不停止

```
docker run -it （images Num）/bin/bash
```

#### 容器操作命令

- 列出当前正在运行的容器
    - -a：列出当前所有正在运行的容器+历史上运行过的
    - -l：显示最近创建的容器
    - -n：显示最近创建的n个容器
    - -q：静默模式，只显示容器编号

```
docker ps [OPTIONS]
```

- 容器启动命令

```
docker start [images ID]
```

- 容器停止命令

```
docker stop [images ID]
```

- 容器删除
    - -f：强制

```
docker rm [images ID]
```

- 一次性删除多个容器

```
docker rm -f $(docker ps -a -q)
docker ps -a -q | xargs docker rm
```

- 前台交互式启动
    - ctrl+c：停止docker服务

```s
docker run -it [images ID]
```

- 后台运行启动(启动守护式容器)

```
docker run -d [images ID]
```

- 查看日志

```
docker logs [images ID]
```

-  查看容器内部细节

```
docker inspect [images ID]
```

- 查看容器内运行的进程

```
docker top [images ID]
```

- 重新打开终端
    - exit：退出终端，不退出容器
    - ctrl+p+q：退出终端，不退出容器

```
docker exec -it [images ID] /bin/bash
```

- 重新打开终端
    - exit：退出终端，退出容器
    - ctrl+p+q：退出终端，退出容器

```
docker attach [images ID]
```

- 拷贝文件

```
docker cp [images ID] [容器内路径] [主机目的路径]
```

- 创建本地新容器，改一版新的镜像放到docker images里，稍后可以用来push  （重要）

```
docker commit -m="add ifconfig" -a="adv" 37ee7d4813be ubuntuifconfig:1.2
```

- docker推送到云端

```
docker tag [images ID] [阿里云镜像仓库地址]:[TAG]
```

- 私服镜像下载docker本地仓库
    - 也是一个容器，用于push容器到本地docker仓库

```
docker pull registry
```

- 修改端口IP

```
docker tag zzyyubuntu:1.2 [容器内部IP]:5000/name:1.2
```

- 推送到本地镜像仓库

```
curl -XGET http://172.17.0.3:5000/v2/_catalog
```

- 不晓得干了啥

> 效果是run容器

```
docker run -d -p 5000:5000 -v /xuwei/myregistry/:/tmp/registry --privileged=true registry
```



## 账号相关

### 阿里云账号登入

```
docker login --username=喂喂喂喂喂 registry.cn-hangzhou.aliyuncs.com
```

### 目前不晓得在干啥

> 效果是 docker iamges 又多增加了一条镜像
>
> 本地和云端的镜像一模一样，包括名称、TAG、ID
>
> 

```
docker tag [ImageId] registry.cn-hangzhou.aliyuncs.com/xwdinguagua/testdemo:[镜像版本号]
```

### 从本地推送到云端仓库

> 放到云端之后会被压缩，但pull回来依旧是原来的体积

```
docker push registry.cn-hangzhou.aliyuncs.com/xwdinguagua/testdemo:[镜像版本号]
```



## docker file



## docker compose



## 案例



## 可视化工具

