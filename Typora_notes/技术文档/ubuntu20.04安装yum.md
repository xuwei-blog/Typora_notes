# ubuntu20.04安装yum



## 报错

```
Command ‘yum’ not found, did you mean:
...
```



## 理论支持

> `apt-get`属于ubuntu、Debian的包管理工具
>
> `yum`则属于Redhat、Centos包管理工具



## 解决方式

1. 尝试直接  apt-get install build-essential  ； apt-get install yum  ， 但无法正常安装

2. 先换了个源

    [清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/)

    - 点击问号，问号里面才是镜像的软件源

    ![image-20240130145743739](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401301457813.png)

    - 原来的软件源进行备份

    ```
    sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
    ```

    - 修改软件源

    ```
    sudo vim /etc/apt/sources.list
    ```

    - 再添加一行地址，必须放到第一行

    ![image-20240130150035216](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202401301500280.png)

    - 更新软件源

    ```
    sudo apt-get update
    ```

    

3. 第二次尝试装yum ，sudo apt-get install yum ，依旧装不上

4. 根据报错，装aptitude ， 再补全python的一些依赖

5. 最后  aptitude install yum ，安装完成

6. 查看版本 yum --version



## 后续研究方向

> apt-get 和 aptitude的异同