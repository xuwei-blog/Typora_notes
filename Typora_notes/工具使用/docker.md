# docker

[TOC]

> b站尚硅谷 阳哥

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

- 修改镜像，使其复合上传要求

```
docker tag ubuntuifconfig:1.3 0.0.0.0:5000/myulocal:1.3
```

- 推送到本地镜像仓库

    - 实测有报错，应该是防火墙问题，还未解决

    - 报错解决，私服库IP就是docker ps显示的

    - push之前要tag新格式
    
        ![image-20240204114001753](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402041140933.png)
    
        ![image-20240204114311958](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402041143055.png)


```
curl -XGET http://0.0.0.0:5000/v2/_catalog
```

- 不晓得干了啥

> 效果是run容器
>
> 把registry容器打开，为了将镜像上传到本地私服库

```
docker run -d -p 5000:5000 -v /xuwei/myregistry/:/tmp/registry --privileged=true registry
```

- 上传镜像到本地私服库

```
docker push 0.0.0.0:5000/myulocal:1.4
```

- 让docker采用https

```
root@ubuntu:/# docker push 0.0.0.0:5000/myulocal:1.3
The push refers to repository [0.0.0.0:5000/myulocal]
Get "https://0.0.0.0:5000/v2/": http: server gave HTTP response to HTTPS client
```

> vim /etc/docker/daemon.json
>
> 添加一行json，刷新重启服务，看下registry有没有打开
>
> systemctl daemon-reload
>
> systemctl restart docker.service

```
"insecure-registries": ["0.0.0.0:5000"]   #私服库IP：端口
```

> 效果展示，push成功
>
> 可以看出镜像是一层套一层的，镜像的分层结构

```
root@ubuntu:/# docker push 0.0.0.0:5000/myulocal:1.3
The push refers to repository [0.0.0.0:5000/myulocal]
e806ade82d1c: Pushed 
9f54eef41275: Pushed 
1.3: digest: sha256:f3a011c40b93ae2c50ebea50ee8fde91282745dd0b41b14242f16c12bafffe98 size: 741
```

- 验证一下有没有上传成功

```
root@ubuntu:/# curl -XGET http://0.0.0.0:5000/v2/_catalog
{"repositories":["myulocal"]}
```

- 拉取私服库镜像

```
docker pull 0.0.0.0:5000/myulocal:1.3
```



- 查看数据卷是否挂载成功

```
docker inspect [images id]
```

> 挂载情况

```
"Mounts": [
    {
        "Type": "bind",
        "Source": "/tmp/docker_host_data",
        "Destination": "/tmp/docker_data",
        "Mode": "",
        "RW": true,
        "Propagation": "rprivate"
    }
```



## 账号相关

### 阿里云账号登入

```
docker login --username=喂喂喂喂喂 registry.cn-hangzhou.aliyuncs.com
```

### 复制镜像并改名

> 效果是 docker iamges 又多增加了一条镜像
>
> 本地和云端的镜像一模一样，包括名称、TAG、ID
>

```
docker tag [ImageId] registry.cn-hangzhou.aliyuncs.com/xwdinguagua/testdemo:[镜像版本号]
```

### 从本地推送到云端仓库

> 放到云端之后会被压缩，但pull回来依旧是原来的体积

```
docker push registry.cn-hangzhou.aliyuncs.com/xwdinguagua/testdemo:[镜像版本号]
```



## 集群

> 1. 集群的Hash槽有区间，单机命令放在集群上可能不适用
> 2. 主从机切换，主机宕机自动切到从机，把主机修好启动，再重启从机，又能回到主机
>
> 

- 查看主从信息

> 查看主从信息

```
redis-cli --cluster check 192.168.111.167:6381
```

- 集群洗牌，重新分配Hash槽

> 新的哈希槽容量 = 16384 / 新的master数量
>
> 每个旧主机给新主机匀了一些空间

```
redis-cli --cluster reshared 192.168.111.167:6381
```

- 添加主机的从机，扩容

```
太长了，用得到再找，关键词 add-node
```

- 删除主从机，缩容

> 先删除从机 del-node，把槽号分配给其他node，再删除主机

![image-20240218104429934](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402181044131.png)



## Dockerfile

> 按照Dockerfile的命令，将老镜像生成新的镜像

### 保留字

- 需要再学

### 构建镜像

> 把想要的操作加进Dockerfile
>
> TAG后面     有个空格，有个点

```
docker build -t centosjava8:1.5 .
```

- 虚悬镜像的构建

> 虚悬镜像没用处，白白占着空间，可以删除

![image-20240218165945142](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402181659209.png)

- 查找虚悬镜像

```
docker image ls -f dangling=true
```



- 删除虚悬镜像

```
docker image prune
```



## docker network

### 查看网络

```
docker network ls
```

### 查看网络帮助

```
docker network --help
```

### 查看网络具体信息

```
docker network inspect XXX（具体的网络name）
```

### 删除网络

```
docker network rm XXX（具体的网络name）
```

### bridge

> 容器会用一个独立的network namespace，容器虚拟出网卡



### 默认网桥docker0

> docker服务给宿主机提供了默认网桥docker0，用于容器与容器，容器与宿主机之间的通讯

- docker服务启动后打开网桥docker0

```
docker network ls
docker network inspect bridge    #此时可以看到已开启默认网桥
```



![image-20240219134144200](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402191341512.png)



### host

> 1. 容器不会获得独立的network namespace ，与主机公用一个network namespace，容器将不会虚拟出自己的网卡，而是使用宿主机的IP和端口
> 2. 当--network=host或者-net=host时，在host模式下，如果指定了-p端口映射，-p设置的参数不会有作用，端口号会以主机端口号为主，重复时递增
> 3. 解决办法就是用bridge模式

- 语法

```
#有警告的写法
docker run -d -p 8081:8080 --network host --name u1 image1
#正确写法,别写-p
docker run -d              --network host --name u1 image1
```



### network none模式

> 只有1个本地   lo  网络 



### container网络模式

> 借用其他容器的网络，但文件系统、进程列表还是隔离的

![image-20240219145349327](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202402191453432.png)



- 端口冲突案例

```
## app85是默认网桥，app86容器借用app85的网络配置，会造成端口冲突
docker run -d -p 8085:8080                           --name app85 image
docker run -d -p 8086:8080 --network container:app85 --name app86 image

## 假设没有冲突，关闭app85，app86的网络也会消失
```



## 自定义网络模式

> 1. 在同一个网段下，ping IP可以，但不能ping 服务名
> 2. 需要用到自定义网络，启动容器并加入自定义网络，就可以通过服务名互通

- 语法

```
docker run -d -p 8081:8080 --network xw_network --name app81 image
docker run -d -p 8082:8080 --network xw_network --name app82 image

## 进入容器互动终端，可以通过服务名ping通
root@app81：/pwd # ping app82   
```



## docker compose









## 案例









## 可视化工具

