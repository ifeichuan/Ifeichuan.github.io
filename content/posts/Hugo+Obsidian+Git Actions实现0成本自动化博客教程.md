---
title: Hugo+Obsidian+Git Actions实现0成本自动化博客教程
tags: [博客,教程,Github]
date: 2023-07-15 18:10:09
draft: false
hideInList: false
isTop: false
feature: 
---

借鉴：

- [obsidian 配合 hugo、cloudflare：让发布博客简单到不可思议 :: 夜猫日记](https://lillianwho.com/posts/obsidian-hugo-cloudflare/)
- [Hugo + Github Actions 实现自动化部署 :: 木木木木木](https://immmmm.com/hugo-github-actions/)

## 需求

- 想搭博客但是很穷捏！
- 习惯用 Obsidian 写东西
- 嫌麻烦

## 怎么做？

首先我们需要最基本的环境和账号。

github 的账号这里不再赘述，自己动手。

Git 的安装可以参考这篇：[Git 详细安装教程（详解 Git 安装过程的每一个步骤）\_git 安装\_mukes 的博客-CSDN 博客](https://blog.csdn.net/mukes/article/details/115693833)

### 安装 Hugo

第一步，进入官网下载：[Releases · gohugoio/hugo](https://github.com/gohugoio/hugo/releases)

**下载这个**（一定得是这个！)

![image.png](https://s2.loli.net/2023/07/15/AcD67igBLKurtWe.png)

下载解压到你认为合适的目录，这里推荐 C 盘，然后复制路径

![image.png](https://s2.loli.net/2023/07/15/cVWLCAx49Fr67ef.png)

解压完后打开环境变量

![image.png](https://s2.loli.net/2023/07/15/3cSFTQLXVIs86v1.png)

点编辑，新建，**Ctrl+C** 完事。

接下来打开终端或 CMD（目前应该终端比较多）

输入`Hugo Version`
![image.png](https://s2.loli.net/2023/07/15/Jlnv64p5t32VmIP.png)
出现上图即为成功。

然后下载源码（不要脸的贴了自己的 😳）[GitHub - ifeichuan/Ifeichuan.github.io: My blog](https://github.com/ifeichuan/Ifeichuan.github.io)
在 Github 上新建 Pages 仓库
将其同步到本地，这里推荐 Vscode 操作。

将源码解压到本地仓库目录。如图：
![image.png](https://s2.loli.net/2023/07/15/ORpP37nkVaKNiTc.png)

可能会少点文件夹，不必在意。

然后我们用 Obsidian 打开仓库文件夹，
安装 Git，Quickadd 插件
设置如图：
![image.png](https://s2.loli.net/2023/07/15/WQGiorblN3wSh7O.png)

然后新建`_Templates`模板文件夹,新建`模板.md`文件
格式如下

```
---
title: {{NAME}}
tags: [{{VALUE:tag？}}]
date: {{DATE:YYYY-MM-DD HH:mm:ss}}
draft: true
hideInList: false
isTop: false
feature:
---

```

打开 quickadd 插件，
![image.png](https://s2.loli.net/2023/07/15/ulZa7QGBhyCpOEn.png)

设置完成后将其同步到**远程仓库**

![image.png](https://s2.loli.net/2023/07/15/ORNlyLUqIhnu7GF.png)
点击 Actions

点击 New workflow

搜索 hugo

![image.png](https://s2.loli.net/2023/07/15/NasUDVtjAoSXHiQ.png)
点这个,无脑点就行。
![image.png](https://s2.loli.net/2023/07/15/lhkeF8os9OmxTyZ.png)

然后你应该就能看到Actions在构建了。构建完成后访问url即可看到自己的博客。


## 后记

做完上面这些后我们只有一个基础的模型，这里推荐一些插件和设置

1. 如果你觉得github提供的域名太长的话，你可以自己购买域名，将其解析到Github
2. Obidian推荐装以下插件，改善使用体验：
	1. 盘古 Pangu 中英文加空格
	2. Auto link title 为链接添加网页标题
	3. Image Auto upload plugin 图片自动上传，搭配[PicGo](https://picgo.github.io/PicGo-Doc/zh/)使用

还有更多请参看开头的链接qwq
