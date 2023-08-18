# windows上使用FTP服务

[TOC]

> 操作环境：win11

## 步骤

1. 打开控制面板，找到`程序和功能`

![image-20230818133328253](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181333521.png)

2. 单机 `启用或关闭Windows功能`

![image-20230818133422518](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181334590.png)

3. 打开FTP服务 和 IIS管理控制台

![image-20230818133649602](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181336638.png)

4. 右击`此电脑` ，左击`管理` ，进入`计算机管理`界面 ， 新建FTP站点

![image-20230818134153843](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181341914.png)

5. 填写站点信息

![image-20230818134330833](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181343870.png)

![image-20230818134544483](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181345523.png)

![image-20230818134604363](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181346405.png)

6. 新建用户，如果提示密码不符合要求，则参照第7步修改策略，注意：==入域的设备修改不了，只能提升密码强度==

![image-20230818134952427](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181349475.png)

![image-20230818135621115](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181356206.png)

7. 打开`本地组策略编辑器`,禁用`密码复杂度策略`，入域设备修改不了

![image-20230818140856751](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181408794.png)

8. 允许FTP通过防火墙，允许svchost应用程序通过防火墙

![image-20230818143641880](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181436940.png)

![image-20230818143814982](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/202308181438029.png)

9. 打开cmd

不晓得为啥，连不上了，截图不放了，分享点我用到的命令，下载的文件会放到c盘user下

```cmd
ftp
open 192.168.1.10
dir
ls
put <文件名>
cd .
```



## 有机会再补充完善