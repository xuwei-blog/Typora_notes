

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

### 恢复为未暂存的状态

```git
git reset HEAD <name>
```

### 添加版本

```markdown
git commit -m "描述信息"
```

### 撤销提交远端仓库

第一次提交撤销不了，后面就可以了，head~ : 倒数第一次的提交   head~2 : 倒数第二次的提交  

--soft  ： 只撤销commit的操作，保留 add

```git
git reset head~ --soft
```

如果不加 --soft  ，就没有在暂存的状态

```git
git reset head~
```

### 删除远程仓库文件

-r 是递归的意思，当最后面是文件夹的时候有用，单个文件不需要-r

```git
git rm -r --cached xxx.txt
```

同时删除远程和本地的文件，慎用！！！

```git
git rm xxx.txt
```



### 查看版本状态

```markdown
git status
```

### 查看提交文件的区别

```git
git diff
```

### 查看版本记录（日志）

``` 
git log		//查看几条log
git reflog	//查看多条log
git log --pretty  //美化一下输出
git log --graph   //图形化展示
git log --pretty=format:"%h , %an , %ar , %s"
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

### 给仓库别名重命名

将远程仓库名origin  重命名为origins

```git
git remote rename origin origins
```

### 修改远程仓库地址

```git
git remote set-url origin <remote-url>
```



### 向远程推送代码

向远程仓库origin 推送本地master分支

```markdown
git push origin master
```

如果觉得这样推送麻烦

```git
git push -u origin master
```

往后就可以用更简洁的命令

```git
git push
```

### 提交脏文件

代码写到一半，需要切换分支改bug，此时切换不了，要不就commit(不推荐)，要不就stash

```git
git stash
```

后续改完bug，恢复代码环境

```git
git stash apply
```

如果断断续续提交脏文件

```git
git stash push
```

查看脏文件记录

```git
git stash list
```

恢复之前的脏文件,最新的是stash@{0}

```git
git stash apply stash@{2}
```

删除之前的脏文件，记录序号往前顺延

```git
git stash drop stash@{2}
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

