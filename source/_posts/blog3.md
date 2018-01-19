---
title: 个人分享
date: 2018-01-17 09:58:26
tags: python
---

人生苦短，我用python。
{% asset_img pic1.jpg %}
<!-- more -->

## 简介
关注python是因为最近网上看到了微信小游戏跳一跳、抢火车票的各种辅助软件、外挂大多都是由python写的，于是挺好奇便对这门语言产生了兴趣。

网上有很生动的比喻说：
汇编能够让你看得很远（了解各种计算机工作原理），但是遇见任何问题都要冲上去肉搏。
C语言终于能够发射子弹了...但是你需要自己敲击底火，C语言所有实现都要写，String类型都要自己实现。
C++算是一件完整的武器了...但是伤人伤己。
python则是全自动战斗机器人，不但能够发射子弹，还能扔枪...
{% asset_img pic2.jpg %}

Python是一种高级编程语言。完成同一个任务，C语言要写1000行代码，Java只需要写100行，而Python可能只要20行。
如批量修改文件名：
```
import os
movie_name = os.listdir('test')

for temp in movie_name:
	new_name='666'+temp
	os.rename('test/'+temp, 'test/'+new_name)
```
(copy过来的Python代码要额外注意，不要看起来代码缩进了就感觉ok了，实际上是没有缩进的。)
像这样的确可以大大提高工作效率，有兴趣有条件的还可以试着做成拥有GUI的小工具。

但代码少的代价是运行速度慢，C程序运行1秒钟，Java程序可能需要2秒，而Python程序可能就需要10秒。

python分为2.X时代和3.X时代，如果是初学者，py3毫不犹豫。
python清晰简洁的语法使得非常适合人类阅读，阅读一个良好的Python程序就感觉像是在读英语一样。Python的这种伪代码本质是它最大的优点之一，它使你能够专注于解决问题而不是去搞明白语言本身。
而且有极其丰富的库，数学计算三件套：numpy，scipy，matplotlib；数据处理库pandas，深度学习库tensorflow等。

提及python，当然要说到爬虫，它拥有很多优秀的网络爬虫库。
如大名鼎鼎的scrapy爬虫框架。scrapy依赖的库比较多，有lxml,zope.interface,pyOpenSSL,Twisted,pywin32。
安装这些库也比较简单，只需用到Python包管理工具Pip就可以了。如在命令行中运行：pip install lxml。
由于不同版本安装后包含的库不同，所以有些库就已经存在了。可以先进入python交互模式输入help("modules")查看已有的库，当然可以直接一个个install也没多大影响。
值得注意的是有些库在pip服务器上没有及时更新，导致不能适用于当前python版本了，就会安装失败，这需要我们去对应库的官网自行下载了。
我的python版本为3.6，当时安装twisted和pywin32都是需要去官网下载，pywin32是一个exe安装程序，可以直接安装；而twisted则是一个whl文件，命令行中还是输入"pip install ",然后把文件拖入回车安装即可。所有依赖库装好了就可以安装scrapy了。

特意附上[scrapy中文文档](http://scrapy-chs.readthedocs.io/zh_CN/latest/)
好了，先不说了，我要学着爬点小黄图了，嘻嘻~

