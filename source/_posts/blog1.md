---
title: 利用 gitPage + hexo 开发自己的博客
date: 2017-08-15 09:58:40
tags:
---
gitPage: 一个可供浏览器访问的静态网页存储空间
[Hexo](https://hexo.io/): 一个快速，简单和强大的博客框架

### 创建gitPage

登录github之后点击右上角的“+”号，选择“New repository”菜单，创建仓库，用于存储和博客相关的源文件。

{% asset_img pic1.png pic1 %}

Repository name需使用自己的用户名，并且名字必须符合这样的规则username.github.io；
其它默认，之后再勾选下面的"Initialize this repository with a README"；
最后点击"Create repository"。

### 环境准备
安装**Node**和**Git**	(我的版本分别是v4.4.4和v2.11.0.windows.1，后面略去一万字...)

### 安装Hexo
```
npm install hexo-cli -g
```

### 创建hexo工程
```
hexo init blog  
```
创建了一个文件夹blog（此处blog换成你自己想要的名字）

### 运行hexo服务器
```
cd blog		(进入blog目录)
npm install	(安装依赖文件)
hexo server	(可简写为hexo s)
```
hexo服务器地址为命令行提示的地址，一般是http://localhost:4000/


### 生成静态文件
```
hexo generate	(可简写为hexo g)
```
编译后，会出现一个 public 文件夹，将所有的md文件编译成html文件

### 部署博客到服务器
首先要命令行返回到blog目录，按ctrl+c，之后输入y即可
```
hexo deploy	(可简写为hexo d)
```
这一步之后各种报错各种坑，后来在家里的手提解决了，然后第二天回公司台式又崩了。
还是不纠结了，由于一直在使用TortoiseGit，只需要提交hexo g编译后的public文件夹内代码就ok了。（有空有兴趣的同学也可以去踩下坑...）

### 新建博文
```
hexo new "blog-name"
```
即可在 Hexo\source\ _posts 目录中找到"blog-name.md"这个文件。你就可以使用makedown编辑器打开进行编写博客内容了。