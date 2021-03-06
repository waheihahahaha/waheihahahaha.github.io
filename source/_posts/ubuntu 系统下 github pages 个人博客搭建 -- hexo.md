---
title: ubuntu 系统下 github pages 个人博客搭建 -- hexo
date: 2019-03-22 17:36:00
comments: true #是否可评论
categories: blog #分类
toc: true #是否显示文章目
tags:   #标签
	- hexo
	- blog
---



用 hexo 搭建个人博客 
<!-- more -->

# 前言
之前往 github 上提交过东西，自认为写的是个人博客，直到后来听他们说起 github pages ，才发现自己提交到了 repository ，出糗了，尴尬...


不管是对于大牛还是对于新手，写博客都是个好习惯。大牛可以洋洋洒洒把一项技术描述的淋漓尽致，虽然我做不到那样，但可以把自己在学习中遇到的问题和解决的办法记录下来，一则积累经验，二则若能帮到其他网友那真是万幸，望能坚持，若指正错误必感激涕零。

# 写作平台对比
目前来说，我比较了解的博客平台：博客园、CSDN 和 github pages。

其他平台，不甚了解，不妄加评论，以后补充。

这三个平台，个人比较喜欢 CSDN 和 github pages 。博客园感觉界面有点 low ，虽然本人长相一般，但稍稍有点颜控，so...  丑拒。毕竟现在来说，哪个平台的功能都差不多，起码没有哪家能做到一家独大，看着心情舒畅比较重要嘛。

CSDN 和 github pages 感觉都差不多，CSDN 的 SEO 做的好，在百度或者 Google 搜索时比较靠前，阅读量会比较高，从追求阅读量来说是一个不错的选择，广告多的有些过分，界面说不上好吧，不过比博客园强多了。gayhub ？哦不对，是 github ，百度是搜不着的，阅读量自然就 emm... ，不过是一个可以向全世界的程序猿展示自己的平台，逼格较高。相对而言，我还是较为喜欢 github 吧 。

# 搭建准备
git 和 node.js 是必须的准备工作，也是入门必备，若是版本较高的 ubuntu 系统，可以使用较为简单的命令行安装，傻瓜式操作，不过一般给下载的都是最新版本，系统较老或者追求稳定版本的可以去官网自行下载解压安装。虽然听说最新版本使用不稳定，但目前来看好像并没有遇到过这种问题，用起来都一样。不过不要像我一样，命令行安装过 node，又从官网下载安装，结果导致当前管理员和超级用户使用的都不是一个版本，当前管理员安装了 node.js 和 npm ，超级用户只有 node.js 却没有 npm ，后来用的时候老报错误，还不明白怎么改，捣鼓了半天，只能卸载重新安装。

温馨提醒，尽量不要在 root 权限下执行操作，容易搞蹦系统。
##  git 介绍
向自己的 github 上传文件，是需要一点 git 基础的，不懂也没有关系，只需要掌握一些基本操作命令就好了。

可参考廖雪峰老师的 git  教程：[ git 基础学习](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)

## git 安装
打开终端（ 桌面右键 open Terminal 或者 Ctrl + Alt + T ）

输入 git ，查看系统是否已经安装   git

```javascript
// An highlighted block 
 $ git
```
已安装，则跳过此步骤，若提示`The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git`，则执行命令：

```javascript
// An highlighted block 
 $ sudo apt-get install git
```
若系统版本较老，可先从Git官网下载源码：[ git 官网](https://git-scm.com/)
解压后，依次执行命令：`./config`，`make`，`sudo make install`

配置个人信息，设置user name 与 email

```javascript
// An highlighted block 
 $ git config --global user.name "github用户名"
 $ git config --global user.email "你注册的邮箱地址"
```

## node.js 介绍
可参考廖雪峰老师的 node.js 教程：[ node.js 基础学习 ](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/00143450141843488beddae2a1044cab5acb5125baf0882000)

## node.js 安装
打开终端（ 桌面右键 open Terminal 或者 Ctrl + Alt + T ）

输入 node -v ，查看系统是否已经安装   node

```javascript
// An highlighted block 
 $ node -v
```
已安装，则跳过此步骤；若未安装：

法一：  apt-get 命令安装

```javascript
// An highlighted block 
  $ sudo apt-get install nodejs
  $ sudo apt-get install npm
```
**法二**： *第一步*  下载 nodejs 包，node.js 官网下载安装：[ node.js 官网 ](https://nodejs.org/en/)

或

```javascript
// An highlighted block 
 $ wget https://nodejs.org/dist/v10.11.0/node-v10.11.0-linux-x64.tar.xz   //下载
 $ tar xf  node-v10.11.0-linux-x64.tar.xz       // 解压
 $ cd node-v10.11.0-linux-x64/                  // 进入解压目录
 $ ./bin/node -v                               // 执行node命令 查看版本
```
*第二步*   创建软连接，环境变量配置，当前管理员   与  超级用户下都可执行 npm 与 node 

```javascript
// An highlighted block 
  $ ln -s  /home/root/node-v10.11.0-linux-x64/bin/node  /usr/local/bin/
  $ ln -s /home/root/node-v10.11.0-linux-x64/bin/npm  /usr/local/bin/
```
注意：要写文件的绝对路径
举例：我的电脑创建软连接的实际代码如下

```
sudo ln -s /home/wahahaha/.nvm/versions/node/v11.12.0/bin/node /usr/local/bin/
sudo ln -s /home/wahahaha/.nvm/versions/node/v11.12.0/bin/npm /usr/local/bin/
```
电脑中 node 和 npm 的路径如下 ==>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190320202534963.png)

查看是否安装到全局：`sudo node -v`，`sudo npm -v`

# 博客框架搭建
在框架搭建的时候，一般给推荐 jekyll 和 hexo 两种。刚开始还挺纠结，选择困难症这可咋办啊，就去网上看看他们各自的优缺点吧。结果发现全是捧 hexo 贬 jekyll 的，那感觉 jekyll 在 hexo 面前一文不值，根本不用纠结的好嘛，果断选择 hexo。也确实好用：依赖少，使用方便，色调较柔和，生成静态站点速度快 ... 当你完成本地博客的搭建，并成功用浏览器打开时，你已经离成功只有一步之遥了。


## hexo 的介绍与安装

hexo 是一个博客框架，拥有众多博客主题

安装：


```javascript
// An highlighted block
  $ npm install -g hexo-cli
```
开始建站：

```javascript
// An highlighted block
 $ hexo init <folder>
 $ cd <folder>
 $ npm install
```

<folder>  文件夹名称随意，初始化 Hexo 。
生成静态文件命令：`hexo generate`
启动服务器命令：`hexo server`

现在，Hexo 本地博客已经搭建好了，可以用浏览器打开网址：[ http://localhost:4000/](http://localhost:4000/)  进行预览。

# 将本地博客部署到 github

首先，需要注册一个 github  的账号，就像注册一个 QQ 号那样简单，不过由于网页是纯英文的，对于英文不太好的伙伴看起来可能有点费力，不过并不难。然后，需要创建一个你自己的仓库 repositories，且仓库名必须是用户名后面加上`.github.io`，否则不会被识别。
远程连接服务器时，需要 SSH 协议将本地与远程连接服务器时，需要 SSH 协议将本地与远程服务器进行连接，生成的两个文件一个为公钥(id_rsa)一个为私钥(id_rsa.pub)，我们需要把公钥配置到 github 的 SSH 上，当我们与远程连接时，公钥会与私钥相匹配。Deployment 配置是为了 hexo 命令能与用户的 github 对接。
## 账号注册及SSH配置
第一步： github 账号注册，地址：[https://github.com/](https://github.com/)

第二步：注册登录后，创建一个新的repositories，且 Repository name 为：( github 账户名称 ).github.io，例如我的是：< waheihahahaha.github.io >，否则打不开博客主页

第三步：配置 SSH  
生成秘钥：

```
 $ ssh-keygen
```
打开文件：

```
 $ cat ~/.ssh/id_rsa.pub
```
把内容 copy 下来，打开 github 点击右上角头像，点击 settings，点击 SSH ，添加。
判断 SSH 是否配置成功：

```javascript
// An highlighted block
 $ ssh -T git@github.com
```
如果出现 `Hi! You've successfully authenticated, but GitHub
 does not provide shell access.`则配置成功。

## 配置 Deployment
打开创建的 folder，在 _config.yml 中进行如下配置：

```
deploy:
  type: git
  repo: git@github.com:waheihahahaha/waheihahahaha.github.io.git  //waheihahahaha 为自己的账户名称
  branch: master
```

执行命令：
`hexo clean`，`hexo g`，`hexo d`
接下来用浏览器访问：`"用户名".github.io`即可访问自己的博客

# 撰写博客
推荐 [CSDN-Markdown](https://mp.csdn.net/)编辑器，编辑好之后导出放到 sources ->_posts 内，重新执行命令：
`hexo clean`，`hexo g`，`hexo d`

