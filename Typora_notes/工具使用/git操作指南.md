

# git操作指南

## 概述

[TOC]

## git简介

### 什么是git？

- 分布式
- 版本控制
- 软件

### 版本控制软件的发展

1. N个文件
2. 本地文件
3. 集中式版本控制（1个中心）
4. 分布式（不怕服务器挂掉）

### 为什么要用git？

方便回滚到之前的版本

### git流程

1. 进入要管理的文件夹(git bash here)
2. 初始化（给git管理的权限）
3. git进行管理
4. 生成版本

### git管理文件的三种状态

- 红色 新增文件/修改过的文件
- 绿色 已经被管理的文件
- 透明 已经生成版本的文件

### git专业术语

|           工作区           |     暂存区      |       版本库       |
| :------------------------: | :-------------: | :----------------: |
|                            | git add后的区域 | git commit后的区域 |
| 已管理的文件和新修改的文件 |                 |                    |



## git基本指令

### 初始化

```markdown
git init
```

### 添加被管理的文件

```markdown
git add file.md		//添加某一个文件
git add .		//添加所有未被管理的文件
```

### 添加版本

```markdown
git commit -m "描述信息"
```

### 查看版本状态

```markdown
git status
```

### 查看版本记录（日志）

``` 
git log		//查看几条log
git reflog	//查看多条log
git log --graph --pretty=format:"%h %s"   //按格式查看日志
```

### 配置信息

- 上传者信息
- 新安装git不配置会报错

```markdown
git config --global user.email "1319284583@qq.com"
git config --global user.name "xxxxww"
```

### 回滚

```markdown
git reset -hard 版本号
```

![image-20221216001956126](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20221216001956126.png)

## git分支指令

### 查看目前分支

```markdown
git branch
```

### 创建新分支

```markdown
git branch 分支名
```

### 切换分支

```markdown
git checkout 分支名
```

### 合并分支

- 先切换到目的地分支
- 再将目标分支合并过来

```markdown
git merge 分支名
```

### 删除分支

```markdown
git branch -d 分支名
```

## 多人协作指令

### 给仓库起别名

```markdown
git remote add origin 远程仓库地址
```

### 向远程推送代码

```markdown
git push -u origin 分支名
```

### 克隆远程仓库

```MARKDOWN
git clone 远程仓库地址
```

### 拉取仓库代码

```
git pull origin 分支名

以上1条代码等同于以下2条代码

git fetch origin 分支名
git merge origin/分支名
```

### 变基

- 多个记录-->1个记录
- 让git记录简洁
- 减少分支

```
git rebase -i 版本号  //从head到版本号 更新日志合并
```

![image-20221231153353137](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20221231153353137.png)

> rebase操作会修改节点5、7的commit信息

### 解决冲突

1. 安装beyond compare
2. 在git中配置

```
git config --local merge.tool bc3
git config --local mergetool.path '/user/local/bin/bcomp'
git config --local mergetool.keepBackup false

//local -- 只对当前项目有效
 
```

3. 应用beyond compare 解决冲突

## 协同开发

### 流程

gitflow工作流

![image-20221231180627894](https://typora-notes-codervv.oss-cn-shanghai.aliyuncs.com/img_for_typora/image-20221231180627894.png)

## 代码检查

github中  `pull request`

## 贡献代码

1. `fork`别人的仓库到自己的仓库
2. `clone`自己的仓库到本地
3. `new pull request` 提交申请

## 免密登录

### URL登入

```
原来的：https://github.com/vigman-xxxw/cpp-code.git
修改后：https://用户名:密码github.com/vigman-xxxw/cpp-code.git
git remote add origin https://用户名:密码github.com/vigman-xxxw/cpp-code.git
```

### SSH

1. 生成公钥和私钥

```
ssh-keygen
```

- id_rsa.pub公钥
- id_rsa私钥

2. 拷贝公钥的内容，放到github中
3. 在本地配置ssh地址

```
git remote add origin git@github.com:vigman-xxxw/cpp-code.git
```

## 忽略文件

```
*.h     //忽略所有.h结尾的文件
!a.h    //忽略除了a.h
files/  //忽略文件名
```

