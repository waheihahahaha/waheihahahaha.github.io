---
title: An Elegant Static Blog Generator ———— 使用 github pages 和 hexo 搭建个人博客
date: 2019-03-27 17:34:18
tags:
---


# 摘要

An elegant static blog generator 意为一个简洁的静态博客生成器，目的是为博客创作者提供便利。

这个静态博客生成器主要由两部分构成：github pages 和 hexo。Github pages 是供用户实现托管服务的一个静态网站，hexo 则是一个简洁、高效的博客框架。

今天我们的目的就是`使用 github pages 和 hexo 搭建用户自己的个人博客`，以下配置均在 `ubuntu` 系统下进行。

# 前言
之前往 github 上提交过东西，自认为写的是个人博客，直到后来听他们说起 github pages ，才发现自己只是提交到了新的仓库（repository）里面 ，出糗了，尴尬...


> 我们为什么要写博客呢？

写博客的好处有很多，打个比方，我们需要学习一项新的技术，在学习的过程中可能会遇到很多的坑，我们可以记录填坑经历或者写一篇技术总结，一是为了让自己更加熟练，二则可以帮助后来者少走一些弯路，再则有可能许久不用，一年半载后忘却了这项技术，我们可以通过这篇博客把忘记的快速捡起来。

写博客是个好习惯，不管对于大牛来说还是对于一个新手。大牛可以洋洋洒洒把一项技术描述的淋漓尽致，虽然我做不到那样，但可以把自己在学习中遇到的问题和解决的办法记录下来，一则积累经验，二则若能帮到其他网友那真是万幸，望能坚持。

> 那么，我们为什么要用 github pages 和 hexo 搭建个人博客呢？

目前来说，我比较了解的博客平台：博客园、CSDN 和 github pages 。至于其他平台，不甚了解，不妄加评论，以后补充。这三个平台来讲，我认为 github pages 是比其他两个平台要好的多的 。

博客园 和 CSDN 的 SEO 做的不错，在百度搜索或者 Google 时排名比较靠前，阅读量相对来说会比较高。但是博客园的界面做的实在不怎么样，毕竟现在来说，每个平台的功能都差不多，起码没有哪家能够做到一家独大，看着心情舒畅还是比较重要的。CSDN 的界面比博客园强不了多少，而且广告多的有些过分，周围各种广告弹窗骚扰，实在谈不上是好的体验。而 github 在这方面做的就好的多，界面简洁无广告，并且面向的是全世界的程序猿，可以更好的展示自己， `github pages 明显是一个好的选择。`

我们在写博客之后，需要有一个转换器，把我们写的东西编译成一个 web 界面用于显示。目前比较流行的编译器有 jekyll 和 hexo，github pages 官方推荐的是 jekyll ，但是 jekyll 本身使用 ruby 写的，需要有 ruby 基础，而 hexo 是用 js 写的，编译速度也会比 jekyll 快一些。如果你了解或者想了解 ruby，那么就用 jekyll ，我自己不用 ruby，想做一些修改的话会很麻烦，还不如换一种比价熟悉的，学过一些 js，虽然不太熟练，但比 ruby 好一些。所以，`我选择用 github pages 和 hexo 来搭建个人博客。`


# 搭建准备
 
下面说一下需要做的准备工作 -----
 （一）git 的下载与安装
 （二）node 与 hexo 的下载安装
 （三）github 账号注册及 SSH 配置

## （一）git 的下载与安装

***为什么要安装 git***

> gitHub 是一个面向开源及私有软件项目的托管平台，因为只支持 git 作为唯一的版本库格式进行托管，故名 gitHub。-----（来自百度百科）

也就是说，我们的本地文件需要上传到 github 时，是需要用到 git 的，我们进行代码的拉取或是上传都需要 git 的支持。git 对于 github 来说是必须的准备工作，乃入门必备，我们需要下载安装 git ，还需要一点 git 基础，需要掌握一些基本的操作命令。

可参考廖雪峰老师的 git  教程：[ git 基础学习](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)

***git 安装*** 

若是版本较高的 ubuntu 系统，可以直接使用命令行安装，操作简单，下载的都是最新版本。若系统版本较老，可自行从Git官网下载源码：[ git 官网](https://git-scm.com/) 进行安装，这边不做介绍。

打开终端（ 桌面右键 open Terminal 或者 Ctrl + Alt + T ）

输入 git ，查看系统是否已经安装   git

```javascript
// An highlighted block 
 $ git  // 查看是否进行过 git 安装
```
若显示版本，则已安装，跳过此步骤，若提示`The program 'git' is currently not installed. You can install it by typing: sudo apt-get install git`，则执行命令：

```javascript
// An highlighted block 
 $ sudo apt-get install git  //安装 git
```

>释义：
> sudo 是 linux 系统的管理指令，允许普通用户执行一些 root 命令的工具； 
> apt-get 是一条 linux 指令，适用于 deb 包管理式的操作系统，需要 root 权限，所以一般跟着 sudo 命令； 
> 温馨提醒，不要在 root 权限下执行操作，容易搞蹦系统。

***git 个人信息配置***

设置user name 与 email

```javascript
// An highlighted block 
 $ git config --global user.name "用户名"  // 配置用户名
 $ git config --global user.email "邮箱地址"  // 配置邮箱
```

## （二）node.js 、npm 与 hexo 的下载安装

***为什么要安装 node.js 、npm与 hexo***

hexo 前面我们提到过，是一个简洁的博客框架，我们需要下载安装 hexo 。但是，hexo 的安装是基于 node.js 的，在下载 hexo 之前，我们需要先下载安装 node.js  。npm 则是 node.js 的包管理工具，我们在进行开发时，如果需要用到别人封装好的包，可以直接通过 npm 下载安装，还会把我们需要使用的所有依赖的包进行下载管理，比程序员手动管理要好的多，简单又不容易出错。

如果想进一步了解可参考 廖雪峰老师的教程：[ node.js 基础学习 ](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434501245426ad4b91f2b880464ba876a8e3043fc8ef000)  或 hexo 文档：[ hexo](https://hexo.io/zh-cn/docs/)

***node.js 与 npm 安装***

这边同 git ，可以直接使用命令行进行安装，操作简单，若是系统版本较老，可自行从 node.js 官网下载稳定版本：[ node.js 官网](https://nodejs.org/zh-cn/) 进行安装，这边不做介绍。

打开终端（ 桌面右键 open Terminal 或者 Ctrl + Alt + T ）

输入 `node -v` 和 `npm -v`，查看系统是否已经安装   node.js 和 npm 。
```javascript
// An highlighted block 
 $ node -v  // 查看 node 版本
 $ npm -v   // 查看 npm 版本
```

若显示版本，则已安装，跳过此步骤；若未安装，则可以使用 curl 安装：

> 释义：
> curl 命令可以直接获得到指向的页面，
> 如果这个 URL 指向的是文件或是图片，直接下载到本地

1. 安装 curl

```javascript
$ sudo apt-get install curl
```

2. 安装 node.js 和 npm
npm 会在 node.js 安装的时候顺带安装

```JavaScript
$  curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
$  sudo apt-get install -y nodejs  
```
3. 查看安装版本

```javascript
 $ node -v  // 查看 node 版本
 $ npm -v   // 查看 npm 版本
```
4. 查看是否安装到全局
```javascript
 $ sudo node -v  // 查看 node 版本
 $ sudo npm -v   // 查看 npm 版本
```

***hexo 安装***

hexo 是一个快速、简洁且高效的博客框架，使用命令安装：

```javascript
// An highlighted block
  $ npm install -g hexo-cli  // hexo 安装
```
查看是否安装成功
```javascript
// An highlighted block
  $ hexo -v  // 查看 hexo 是否安装成功，显示版本，则安装成功
```

***hexo 建站***

hexo 建站是指使用 hexo 在本地成功搭建博客，当你完成本地博客的搭建，并成功用浏览器打开，那么离成功只有一步之遥了。

首先新建一个文件夹（文件夹必须是空的），
打开终端（ 桌面右键 open Terminal 或者 Ctrl + Alt + T ），
开始建站：

```javascript
// An highlighted block
 $ cd <folder>  // 进入当前文件夹，folder 为新建文件夹的文件名，可为任意值
 $ hexo init  // 初始化当前文件夹，会在文件下生成所需文件
 $ npm install  // 安装配置文件
```
现在，Hexo 本地博客已经搭建好了，用浏览器打开网址进行预览，依次执行：

```javascript
 $  hexo clean   // 清除缓存文件和已生成的静态文件
 $  hexo g       // 即 hexo generate，生成静态文件
 $  hexo s       // 即 hexo server，启动服务器，默认访问网址为：http：//localhost:4000/
```
访问网址：`http://localhost:4000/` 即可看到自动生成的博客 `hello world`

## （三）github 账号注册及 SSH 配置

首先，需要注册一个 github  的账号，就像注册一个 QQ 号那样简单，不过由于网页是纯英文的，对于英文不太好的伙伴看起来可能有点费力，不过并不难。然后，需要创建一个你自己的仓库 repositories，且仓库名必须是用户名后面加上`.github.io`，否则不会被识别，这也就是个人博客的仓库。
远程连接服务器时，需要 SSH 协议将本地与远程连接服务器时，需要 SSH 协议将本地与远程服务器进行连接，生成的两个文件一个为公钥(id_rsa)一个为私钥(id_rsa.pub)，我们需要把公钥配置到 github 的 SSH 上，当我们与远程连接时，公钥会与私钥相匹配。

***账号注册***

 github 账号注册，地址：[https://github.com/](https://github.com/)

***博客仓库建立***

注册登录后，创建一个新的repositories，且 Repository name 为：( github 账户名称 ).github.io，例如我的是：< waheihahahaha.github.io >，也即博客主页。

 ***SSH  配置***
 
打开终端，生成秘钥：
```javascript
 $ ssh-keygen  // 生成秘钥
```

打开公钥文件，并把公钥配置到 github 上：
```javascript
 $ cat ~/.ssh/id_rsa.pub  // 打开公钥文件
```
把内容复制下来，打开 github 点击右上角头像，点击 settings，点击 SSH ，添加。

判断 SSH 是否配置成功：

```javascript
// An highlighted block
 $ ssh -T git@github.com
```
如果出现 `Hi! You've successfully authenticated, but GitHub
 does not provide shell access.`则配置成功。

# 把本地博客上传到 github 仓库

本地博客上传到 github 仓库，必须建立他们之间的联系，需要更改站点配置文件，即文件根目录下面的 _config.yml文件。最后即可把本地文件通过 hexo 进行上传，把预先生成静态文件部署到 github 。

***配置 Deployment***

Deployment 配置是为了 hexo 命令能与用户的 github 对接。
打开创建的 folder，打开文件 _config.yml ，对 deploy 进行如下配置：

```
deploy:
  type: git
  repo: git@github.com:waheihahahaha/waheihahahaha.github.io.git  //waheihahahaha 为自己的账户名称
  branch: master
```

> 注：repo 行 的 waheihahahaha 为自己的账户名称，自行更改

***文件部署到 github***

在终端，依次执行命令：

```javascript
 $  hexo clean   // 清除缓存文件和已生成的静态文件
 $  hexo g       // 即 hexo generate，生成静态文件 （public 文件）
 $  hexo d       // 即 hexo deploy，部署网站，把本地上一步生成的静态文件部署到 github
```

接下来用浏览器访问：`"用户名".github.io`即可访问自己的博客

# 撰写博客
推荐 [CSDN-Markdown](https://mp.csdn.net/)编辑器，编辑好之后导出放到 sources ->_posts 内，重新执行命令：
`hexo clean`，`hexo g`，`hexo d`
即可把编写好的内容部署到 github





