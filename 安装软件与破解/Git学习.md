# Git学习

## Git介绍

Git是目前世界上最先进的分布式版本控制系统。

## Git与GitHub

Git是一个分布式版本控制系统，简单的说就是一个**软件**，用来记录一个或若干个文件内容变化骂一遍将来查阅特定版本修改情况的软件。

GitHub是一个为用户提供Git服务的**网站**，简单的说就是一个可以放代码的地方。

## Git的使用

### 本地仓库

#### 工作流程

Git本地操作的三个区域：

**工作区（Working Directory）**<br>添加、编辑、修改文件等动作

**暂存区**<br>暂存已经修改的文件最后统一提交到git仓库中

**Git Repository（Git仓库）**<br>最终确定的文件保存到仓库，成为一个新的版本，并且对他人可见

![Git工作流程](https://raw.githubusercontent.com/qingyunlyp/picstore/master/img/202210121118741.jpg)

#### 本地仓库操作

`仓库有名版本库，英文名repository，可以简单的理解成一个目录，用于存放代码，这个目录所有文件都可以被Git管理起来，给个文件的修改删除等操作Git都能找到`

安装好Git之后首次使用需要先进行**全局配置**

打开Git命令窗口

```shell
git config --global user.name "输入自己的用户名"
git config --global user.email "输入自己的邮箱"
```

#### 创建仓库

当我们需要让Git去管理某个新项目/已存在项目的时候，就需要创建仓库。<br/>**注意**：尽量不要出现中文

#### Git仓库初始化

让Git知道管理仓库<br>指令：`git init`<br>

```shell
git init
```

#### git常用指令

##### `git status`   查看当前状态

##### `git add 文件名`  添加到缓冲区

`git add`指令可以添加一个文件，也可以添加多个文件

```sh
git add 文件名  //添加一个文件
git add 文件名1 文件名2...  //添加多个文件
git add .    添加多个文件
```

##### `git commit -m "注释内容"`  提交到版本库

#### 版本回退

##### 1.查看版本`git log`

```sh
git log   
git log --pretty=oneline
两者都是显示版本信息的区别是 `--pretty=oneline`是：在一行显示版本号和注释 
```

![image-20221013161048935](https://raw.githubusercontent.com/qingyunlyp/picstore/master/img/202210131610988.png)

##### 2.回退指令 `git reset --hard 提交编号`

##### 3.查询历史操作 `git reflog`

![image-20221013195720234](https://raw.githubusercontent.com/qingyunlyp/picstore/master/img/202210131957280.png)

```
注意：
1.要想回到过去，必须先得到commit id 然后通过`git reset --hard 提交编号` 进行回退
2.要想回到未来，需要使用`git reflog`进行历史操作查看，得到最新的commit id。
3.写回退指令时，commit id可以不用写全，git会自动识别，但也不能也太少，只收需要写前4位字符
```

### 线上远程仓库--两种常用的使用方式

1. 基于http协议
2. 基于SSL协议

#### 基于http协议

##### 使用`clone`指令将项目克隆到本地

![image-20221013205346470](https://raw.githubusercontent.com/qingyunlyp/picstore/master/img/202210132053516.png)

##### 在仓库上的对应操作

###### 提交暂存区`git add 文件名`

###### 提交本地仓库`git commit -m "注释内容"`

###### ==提交==线上仓库`git push`

###### ==拉取==线上仓库`git pull`

#### 基于SSL协议


