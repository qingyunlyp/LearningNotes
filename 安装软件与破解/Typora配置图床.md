# Typora配置图床

`图床就是互联网中存储图片的空间。假设你在微博分享一张图片，你的粉丝可以通过互联网看到你分享的图片，那么他是去访问你的手机的相册吗？其实不是的，你分享图片，也就是把图片上传到微博的服务器，微博将为你生成一个独一无二的访问链接，这个链接指向的空间其实就是图床。`

## 图床平台

`图床平台很多，各有优缺点。`

### 1.gitee图床

**优点：**免费稳定，简单易用

**缺点：**只支持单张 1 MB 以内大小的图片，单个免费图床大小上限为 500 MB，图片安全性较差，图床存在一定的失效风险

### 3.GitHub图床

一个免费图床，设置也是比较简单，但是因为在国外，速度很慢，加载一张图片要10秒左右，所以并不太推荐。

### 2.SMMS图床

**优点：**免注册永久存储，图片链接支持https，可以删除上传的图片，提供多种图片链接格式，开放了API，无广告；

**缺点：**图片上传限制，每个图片最大5M，每次最多上传10张，免费最大空间为5G，操作有点繁琐，界面为英文。



## 准备工作

下载软件，电脑上要有`Typora`和`PicGo`或者相似的软件，我想原理基本都一致。

支持`PicGo`版本：≥0.9.84（beta）。需要配合`Node.js`使用

### 安装`Node.js`

官网下载 https://nodejs.org/zh-cn/download/

![2022-10-11_092624](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210110926554.png)

### 安装`PicGo`

在`GitHub上`下载：https://github.com/Molunerfinn/PicGo

| 下载源                                             | 地址/安装方式                                                | 平台       | 备注                 |
| -------------------------------------------------- | ------------------------------------------------------------ | ---------- | -------------------- |
| GitHub Release                                     | https://github.com/Molunerfinn/PicGo/releases                | All        | 国内下载速度可能会慢 |
| [腾讯云COS](https://cloud.tencent.com/product/cos) | https://github.com/Molunerfinn/PicGo/releases 附在更新日志结尾 | All        |                      |
| [山东大学镜像站](https://mirrors.sdu.edu.cn/)      | https://mirrors.sdu.edu.cn/github-release/Molunerfinn_PicGo  | All        |                      |
| [Scoop](https://scoop.sh/)                         | `scoop bucket add helbing https://github.com/helbing/scoop-bucket` & `scoop install picgo` | Windows    |                      |
| [Chocolatey](https://chocolatey.org/)              | `choco install picgo`                                        | Windows    |                      |
| [Homebrew](https://brew.sh/)                       | `brew install picgo --cask`                                  | macOS      |                      |
| [AUR](https://aur.archlinux.org/packages/yay)      | `yay -S picgo-appimage`                                      | Arch-Linux |                      |

![2022-10-11_100820](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111011126.png)

GitHub慢的话可以直接用我下载的安装包（Windows平台）

百度网盘链接为：

链接：https://pan.baidu.com/s/1rN31RG8J7tdK3PqDFQUEZQ?pwd=6var 
提取码：6var

![2022-10-11_085947](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210110927867.png)

### 安装`Typora`

现在最高版本是1.4.8，需要激活。在网络上找到一种激活方式，没有激活这个版本。以下链接是1.2.4版本的一种激活方式以及安装包。

链接：https://pan.baidu.com/s/15LLGEgJkALilQEYnk8oqVA?pwd=ybm2 
提取码：ybm2

## 设置Typora

打开`文件`→`偏好设置`→`图像`，然后按照如下图所设置

1. 插入图片时选择`上传图片`
2. 上传服务选择`PicGo(app)`
3. PicGo路径选择`Typora的路径`

![image-20221011131719404](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111317464.png)



## 设置图床

### gitee图床

#### 1.创建仓库

```
仓库名称：picstore
仓库介绍：图床
勾选初始化仓库
选择分支模型：单分支模型(只创建`master`分支)
创建完成之后需要初始化`readme`文件
```

![image-20221011140836183](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111408268.png)

初始化`readme`文件

![image-20221011141124816](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111411886.png)

进入`管理`,将是否开源改为开源

![image-20221011141654756](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111416854.png)

创建文件夹用于存储图片

#### 2.申请私人令牌设置token

进入`设置`→`私人令牌`,创建令牌

**创建的令牌要保存好。**

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111421487.png)

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111421446.png)

#### 3.设置PicGo

安装插件，重启一遍软件就会出现gitee的相关设置

![image-20221011143757779](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111437843.png)

设置gitee

- repo：仓库的地址，填写形式为*gitee用户名/gitee仓库名*。此处的用户名是gitee真实的账户名，不是昵称，判断方法为从仓库的克隆地址中获取。![image-20221011144824883](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111448921.png)

- branch：上传到的仓库分支，保持默认即可。
- token：在配置Gitee仓库时生成的私人令牌。
- path：**此处必填**（不填会在图片上传时报错，不知道为什么）。
- customPath\customUrl：不用管。
- 一定要`设为默认图床`

![image-20221011144051673](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111440729.png)

之后回到进行测试Typora即可。

------

### SMMS图床

进入[官网](https://sm.ms/)，注册账号，申请`API Token`

![image-20221011153727870](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111537928.png)

回到PicGo，下载SMMS插件，重新打开软件PicGo。

![image-20221011154038526](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111540598.png)

将在smms官网申请的`API Token`填写上之后，进行测试就可以了。

另一个SMMS无法成功，所以使用的这个`SMMS-登录用户`

![image-20221011154146005](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111541057.png)

------

### GitHub图床

（1）创建GitHub仓库：
GitHub使用较广，所以申请GitHub账号的步骤省略，直接开始创建GitHub仓库：

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111924257.webp)

（2）GitHub图床的**“token”获取**：

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111924610.webp)

（3）PicGo中GitHub图床设置：

![img](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111927858.webp)自己设置的域名即后期复制图片网址时链接命名较统一。





![image-20221011184022232](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210111840290.png)

