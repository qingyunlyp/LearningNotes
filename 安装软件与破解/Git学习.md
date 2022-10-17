# Git学习

## Git介绍

Git是目前世界上最先进的分布式版本控制系统。

## Git与GitHub

Git是一个分布式版本控制系统，简单的说就是一个**软件**，用来记录一个或若干个文件内容变化骂一遍将来查阅特定版本修改情况的软件。

GitHub是一个为用户提供Git服务的**网站**，简单的说就是一个可以放代码的地方。

## Git的基本使用

### 本地仓库

#### 工作流程

Git本地操作的三个区域：

**工作区（Working Directory）**
添加、编辑、修改文件等动作

**暂存区**
暂存已经修改的文件最后统一提交到git仓库中

**Git Repository（Git仓库）**
最终确定的文件保存到仓库，成为一个新的版本，并且对他人可见

![](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210121118741.jpg#crop=0&crop=0&crop=1&crop=1&id=HBqiC&originHeight=840&originWidth=1250&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

#### 本地仓库操作
`仓库有名版本库，英文名repository，可以简单的理解成一个目录，用于存放代码，这个目录所有文件都可以被Git管理起来，给个文件的修改删除等操作Git都能找到`

安装好Git之后首次使用需要先进行**全局配置**

打开Git命令窗口
```shell
git config --global user.name "输入自己的用户名"
git config --global user.email "输入自己的邮箱"
```

#### 创建仓库
当我们需要让Git去管理某个新项目/已存在项目的时候，就需要创建仓库。
**注意**：尽量不要出现中文

#### Git仓库初始化
让Git知道管理仓库
指令：`git init`
```shell
git init
```

#### git常用指令

##### `git status`   查看当前状态

##### `git add 文件名`  添加到缓冲区

`git add`指令可以添加一个文件，也可以添加多个文件

```shell
git add 文件名  //添加一个文件
git add 文件名1 文件名2...  //添加多个文件
git add .    添加多个文件
```

##### `git commit -m "注释内容"`  提交到版本库

#### 版本回退

##### 1.查看版本`git log`

```shell
git log   
git log --pretty=oneline
两者都是显示版本信息的区别是 `--pretty=oneline`是：在一行显示版本号和注释
```

![](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210131610988.png#crop=0&crop=0&crop=1&crop=1&id=kfGGl&originHeight=363&originWidth=725&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

##### 2.回退指令 `git reset --hard 提交编号`

##### 3.查询历史操作 `git reflog`

![](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210131957280.png#crop=0&crop=0&crop=1&crop=1&id=kcWXO&originHeight=191&originWidth=743&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

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

![](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210132053516.png#crop=0&crop=0&crop=1&crop=1&id=jlGTk&originHeight=137&originWidth=592&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

##### 在仓库上的对应操作

###### 提交暂存区`git add 文件名`

###### 提交本地仓库`git commit -m "注释内容"`

###### 提交线上仓库`git push`

**作用：**让线上仓库与本地仓库一致

![](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210132108542.png#crop=0&crop=0&crop=1&crop=1&id=hLFVm&originHeight=181&originWidth=656&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

###### 拉取线上仓库`git pull`

**作用：**让本地仓库与线上仓库一致

![](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210132109993.png#crop=0&crop=0&crop=1&crop=1&id=kEiEA&originHeight=117&originWidth=829&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

#### 基于SSH协议
与基于http协议相比区别只是在于鉴权方式的不同。也就是说下载和操作里面的文件时只有链接不同，其他操作基本一致。

- 生成秘钥：`ssh-keygen`

- 秘钥存储目录：C:\Users\用户\\.ssh

- 公钥名称：id_rsa.pub

- 私钥名称：id_rsa

##### 主机秘钥生成（需首先需要[安装 OpenSSH 服务器](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse)）
ssh-keygen -t rsa -C "[1963043600@qq.com](mailto:1963043600@qq.com)"

![](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141346948.png#crop=0&crop=0&crop=1&crop=1&id=cjdtn&originHeight=423&originWidth=658&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

## 分支操作

在开发的时候往往是团队协作，多人进行开发，因此光有一个分支是无法满足多人同时开发的需求的，并且在分支上工作并不影响其他分支的正常使用，会更加安全，git鼓励开发者使用分支去完成一些开发任务。

### 分支相关指令

#### 查看分支：`git branch`

![image-20221014151551248](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141515295.png)

**注意：**当前分支标记`*`

#### 创建分支：`git branch 分支名`

![image-20221014151841490](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141518533.png)

#### 切换分支：`git checkout 分支名`

![image-20221014152601369](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141526412.png)

![image-20221014152810734](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141528776.png)

**注意：**创建分支并切换到该分支`git checkout -b 新分支名`

#### 删除分支：`git branch -d 分支名`

![image-20221014153418545](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141534601.png)

**注意：**切换分支时必须==不在==删除的分支之下。

#### 合并分支：`git merge 被合并的分支名`

## 冲突的产生与解决

**冲突的产生：**未拉取`git pull`，直接进行提交`git push`，但是之前项目被修改。

**冲突的解决：**保存代码，重新进行操作。

## [了解图形化管理工具](https://www.php.cn/tool/git/485210.html)

1. GitHub for Desktop；
2. Source Tree；
3. TortoiseGit；
4. Xcode；
5. Eclipse；
6. Visual Studio；
7. Visual Studio Code

### 独立客户端工具

#### GitHub for Desktop

全球开发人员交友俱乐部提供的强大工具，功能完善，使用方便。对于使用GitHub的开发人员来说是非常便捷的工具。界面干净，用起来非常顺手，上面的这条timeline非常漂亮，也可以直接提交PR。

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141624168.png)

唯一让我失望的是GitHub for Desktop不带三方合并工具，你必须自己手动解决冲突才可以。

– 免费
– 同时支持 Windows 和 Mac：对于需要经常在不同的操作系统间切换的开发人员来说非常方便。
– 漂亮的界面：作为每天盯着看的工具，颜值是非常重要的
– 支持Pull Request：直接从客户端提交PR，很方便
– Timeline 支持：直接在时间线上显示每次提交的时间点和大小
– 支持git LFS：存储大文件更加节省空间和高效
– 不支持三方合并：需要借助第三方工具才行

#### Source Tree

SourceTree是老牌的Git GUI管理工具了，也号称是最好用的Git GUI工具。我的体验是确实强大，功能丰富，基本操作和高级操作都设计得非常流畅，适合初学者上手。

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625691.png)

这个工具很有特色的一个功能就是支持Git Flow，你可以一键创建Git Flow的工作流。Git Flow是非常高效的团队协作模型和流程，Git的一大特色就是灵活轻量的分支，但如何在自己的团队中用好这个功能来匹配自己的研发流程是个问题。内置Git Flow让那些不太熟悉的开发人员也可以很快上手，并且将研发的业务流程固化在工具中，可以说是非常贴心的设计。

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625375.png)

在 Windows 环境下，SourceTree是多语言的，但是不知道为什么我的Mac版总是显示英文。

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625098.png)

– 免费
– 功能强大：无论你是新手还是重度用户，SourceTree 都会让你觉得很顺手。对于非常重度用户，Source Tree还支持自定义脚本的执行。
– 同时支持 Windows 和 Mac 操作系统
– 同时支持 Git 和 Mercurial 两种 VCS
– 内置GitHub, BitBucket 和 Stash 的支持：直接绑定帐号即可操作远程repo

#### TortoiseGit

对这只小乌龟估计没有开发人员会不认识，SVN的超广泛使用也使得这个超好用的Svn客户端成了几乎每个开发人员的桌面必备软件。小乌龟只提供Windows版本，提供中文版支持的，对于中国的开发者来说者绝对是福音。

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625137.png)

小乌龟的文件管理器右键菜单的操作方式对于新手来说非常的容易上手，而且容易理解。

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625945.png)

– 免费
– 只支持Windows操作系统：与文件管理器的良好集成
– 中文界面
– 与TortoiseSVN一脉相承的操作体验

### IDE集成的Git客户端

对于使用IDE进行开发的程序员来说，可以不离开常用的IDE就直接操作源代码管理系统是最好的选择，以下是我对几个常见的IDE集成的git客户端的一点体验。

#### Xcode

苹果的移动端应用体验没得说，但是桌面软件的体验就只能呵呵了。对于XCode里面的Git客户端来说，我只能说：够用！

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625847.png)

这个history的列表也是够简单的了。

#### Eclipse – Egit

作为Java集成开发环境的代表，Eclipse内置了egit这个插件来提供git的集成支持。实话实说，这个插件的功能非常丰富，无论是普通的clone, commit, pull/push操作；还是复杂一些的git flow都有支持。除了颜值差点，其它都还好。

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625669.png)

#### Visual Studio – Git Integration & GitHub Extension

Visual Studio 作为全宇宙最强IDE的名声已经在外，自从2013版本以来一直在针对Git的支持进行改进。如果配合社区版使用的话，也是完全免费的。对于使用Windows作为开发环境的程序员来说，VS里面的Git支持已经相当的完善。

直接克隆github上的repo

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625187.png)

分支和历史记录视图

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625853.png)

CodeLens 集成，可以直接在方法级别上查看git历史

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141626645.png)

#### Visual Studio Code

严格来说，Vscode不能算是IDE，只能算上代码编辑器而已，但是随着vscode上面插件的增加以及对于debugging的良好支持，vscode已经狠接近IDE的使用体验了。另外，vscode可以支持Windows, Mac和Linux操作系统，所以对于不同环境的开发人员来说都非常实用。

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210141625226.jpeg)

## 忽略文件

在项目 目录下有很多万年不变的文件目录，或者有些文件目录即便有改动，也不想让其提交到远程仓库的文档，此时我们可以使用“忽略文件”机制来实现需求。

忽略文件需要创建一个名为`.gitignore`的文件，改文件用于声明忽略文件或不忽略文件的规则，规则对==当前目录及其子目录生效==

**注意：**该文件没有文件名，只有后缀名，没有办法在Windows目录下直接创建，可以通过命令行`touch`来创建。

**常见规则**

### `/目录名/`过滤整个目录  

`/mtk/`过滤名为mtk的整个文件夹

### `*文件类型`  过滤该文件类型的文件

`*.zip`过滤所有.zip文件

### `/文件名` 过滤某个文件

`/mtk/do.c`过滤mtk目录下的do.c文件

### `!文件名` 不过滤某个文件

`!index.html`不过滤index.html

### `#`  以`#`开头的都是注释

`#这是注释`
