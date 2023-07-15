---
title: Hugo+Obsidian+Git Actions实现0成本自动化博客教程
tags: [博客,教程,Github]
date: 2023-07-15 18:10:09
draft: true
hideInList: false
isTop: false
feature: 
---

借鉴：
*   [obsidian配合hugo、cloudflare：让发布博客简单到不可思议 :: 夜猫日记](https://lillianwho.com/posts/obsidian-hugo-cloudflare/)
* [Hugo + Github Actions 实现自动化部署 :: 木木木木木](https://immmmm.com/hugo-github-actions/)

## 需求
* 想搭博客但是很穷捏！
* 习惯用Obsidian写东西
* 嫌麻烦

## 怎么做？

首先我们需要最基本的环境和账号。

github的账号这里不再赘述，自己动手。

Git的安装可以参考这篇：[Git 详细安装教程（详解 Git 安装过程的每一个步骤）\_git安装\_mukes的博客-CSDN博客](https://blog.csdn.net/mukes/article/details/115693833)

### 安装Hugo

第一步，进入官网下载：[Releases · gohugoio/hugo](https://github.com/gohugoio/hugo/releases)

**下载这个**（一定得是这个！)

![image.png](https://s2.loli.net/2023/07/15/AcD67igBLKurtWe.png)

下载解压到你认为合适的目录，这里推荐C盘，然后复制路径

![image.png](https://s2.loli.net/2023/07/15/cVWLCAx49Fr67ef.png)

解压完后打开环境变量

![image.png](https://s2.loli.net/2023/07/15/3cSFTQLXVIs86v1.png)

点编辑，新建，**Ctrl+C** 完事。

接下来打开终端或CMD（目前应该终端比较多）

输入`Hugo Version`
![image.png](https://s2.loli.net/2023/07/15/Jlnv64p5t32VmIP.png)
出现上图即为成功。



然后下载源码（不要脸的贴了自己的😳）[GitHub - ifeichuan/Ifeichuan.github.io: My blog](https://github.com/ifeichuan/Ifeichuan.github.io)
在Github上新建Pages仓库
将其同步到本地，这里推荐Vscode操作。

将源码解压到本地仓库目录。如图：
![image.png](https://s2.loli.net/2023/07/15/ORpP37nkVaKNiTc.png)

可能会少点文件夹，不必在意，后面我会再说。

然后我们用Obsidian打开仓库文件夹，
安装Git，Quickadd插件
设置如图：
![image.png](https://s2.loli.net/2023/07/15/WQGiorblN3wSh7O.png)

然后新建`_Templates`模板文件夹
