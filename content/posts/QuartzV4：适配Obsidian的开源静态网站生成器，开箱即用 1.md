---
title: QuartzV4：适配Obsidian的Hugo主题
tags: [主题,Hugo,Obsidian,Blog]
date: 2023-08-26 00:06:30
draft: true
hideInList: false
isTop: false
feature: 
---

## 前言：

笔者能力较差，详情请看：

[Welcome to Quartz 4](https://quartz.jzhao.xyz/#-get-started)

[GitHub - jackyzha0/quartz: 🌱 a fast, batteries-included static-site generator that transforms Markdown content into fully functional websites](https://github.com/jackyzha0/quartz)

> “[一个人]在门打开的情况下工作会受到各种干扰，但[他们]偶尔也会得到关于世界是什么以及什么是重要的线索。”

Quartz 是一款开源的静态网站生成器，和许多常见的生成器不同的是，它适配 Obsidian，且没有自定义主题。

> PS:Quartz **至少需要  [Node](https://nodejs.org/) v18.14**  才能正常运行

**Quartz 还有 v3 版本，其实就是个 Hugo 主题。**

### 特性：

- 适配 Obsidian
- 全文搜索
- 反向链接
- 关系图谱
- wiki 链接
- 语法支持
- 弹出框预览

感觉很像 Obsidian 的网页版。

让我们康康它的具体模样：

日间模式：
![image.png](https://s2.loli.net/2023/08/26/D3pLim8tcS1rMkU.png)


夜间模式：
![image.png](https://s2.loli.net/2023/08/26/AKfaE1dHs4uS92c.png)

## 开始

Node 如何安装本文不再赘述，有需要请看：[下载 | Node.js](https://nodejs.org/zh-cn/download)

然后在准备创建的文件夹中，打开`终端`（最好是管理员模式），依次输入以下内容：

```cmd
git clone https://github.com/jackyzha0/quartz.git
cd quartz
npm i
npx quartz create
```

然后大概是酱紫

![image.png](https://s2.loli.net/2023/08/26/oQte5gHbUDKXZ49.png)

然后我们输入

```
npx quartz build --server
```

![image.png](https://s2.loli.net/2023/08/26/ZJ7fYG4tBACUucr.png)

未完待续...