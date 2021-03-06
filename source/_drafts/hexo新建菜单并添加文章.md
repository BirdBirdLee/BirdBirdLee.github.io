---
title: hexo新建菜单并添加文章
mylink: hexo新建菜单并添加文章
date: 2021-03-08 23:42:41
tags:
	- hexo
categories:
---

## 两种不同效果对比

## 最终效果

本文章使用的是 `next` 主题，其他主题类似。

以添加「读书笔记」菜单为例，以下是最终效果

### 效果一

菜单点开，里面有相关分类的文章，可一直往该页面增加文章，但不能在该界面加其余陈述。**相当于给某个特定分类在菜单栏建立了个快捷方式**。

![image-20210308234647999](https://tcualhp-notes.oss-cn-hangzhou.aliyuncs.com/img/image-20210308234647999.png)

### 效果二

菜单点开后，只有一篇文章，不能链接其他文章。**可以类比「关于」界面**

![image-20210309001205793](https://tcualhp-notes.oss-cn-hangzhou.aliyuncs.com/img/image-20210309001205793.png)

## 操作步骤

### 1. （效果一、二都要做）新建一个名为 `readNotes` 的页面，命令如下

```sh
hexo new page readNotes
```

取名可随意，哪怕写中文的 `读书笔记` 也是可以的，看个人习惯。

后续：我后面还是直接取了中文的 `读书笔记` 的名字，一个是省事，一个是翻译文件只会翻译菜单的 `readNotes`，可以看到两个效果图中的右侧的分类和标题都还是 `readNotes` 没被翻译。

这时候你会发现 `/source/` 文件夹下多了个 `readNotes` 文件夹，里面有个 `index.md`。

效果二中，`index.md` 类似 `next` 内置的「关于」等界面，里面可以写内容，效果一编辑此文件无效。

### 2. （一、二）在主题配置中开启菜单

#### 效果一

```yml
menu:
	readNotes: /categories/readNotes/ || fa fa-bookyml
```

#### 效果二

```yml
menu:
	readNotes: /readNotes/ || fa fa-book
```

#### 图标问题（一、二）

`fa-book` 是图标的简称，`next` 用的是 Font Awesome 的图标

在官网 [Font Awesome，一套绝佳的图标字体库和CSS框架](https://fontawesome.dashgame.com/) 中搜索喜欢的图标，点击复制即可

![image-20210309001915721](https://tcualhp-notes.oss-cn-hangzhou.aliyuncs.com/img/image-20210309001915721.png)

### 3. 修改语言文件，将 readNotes 翻译为「读书笔记」

原本取的就是中文名的可以跳过这步。

自从 NexT-7.3.0 开始，官方推荐采用数据文件将配置与主题分离，这样我们可以在不修改主题源码的同时完成选项配置、自定义布局、自定义样式，便于后续 NexT 版本更新。

我们原来是通过配置主题下的 `languages` 目录中的 `zh-CN.yml` 文件来对菜单等进行中文翻译的，现在我们可以通过在 `hexo/source/_data/` 下新建数据文件 `languages.yml`，并全文配置如下：（注意注释部分）

```yml
---
zh-CN:	#看这里，把下面的内容（即next主题的原zh-CN文件，向右缩进
		# 然后加个标头zh-CN，使用zh-Hans的同理
  name: 简体中文
  title:
    archive: 归档
    category: 分类
    tag: 标签
    schedule: 日程表
  menu:
    home: 首页
    archives: 归档
    categories: 分类
    tags: 标签
    about: 关于
    search: 搜索
    schedule: 日程表
    sitemap: 站点地图
    commonweal: 公益 404
    readNotes: 读书笔记	#在这里添加
  sidebar:
    overview: 站点概览
    toc: 文章目录
  post:
  #（以下省略，不要直接复制本代码，先缩进，再加zh-Hans或zh-CN标头，再加readNotes: 读书笔记）
```

关于配置文件与主题分离，强烈建议阅读这篇文章：

[Hexo-NexT 版本更新记录 | 小丁的个人博客](https://tding.top/archives/2bd6d82.html)

### 4. （仅一）如果在新建文章时进行归类

写文章时，头部加个 `readNotes` 分类就行，以下是 next 主题的方式

```yml
---
(title, date等其余头部信息已省略)
categories:
  - readNotes
---
```

先在这个分类下写一篇文章，再 `hexo s`，否则会报错。

## 参考

1. 参考了小丁的关于 `next` 主题的数据文件部分，主要是 `languages.yml` [Hexo-NexT 版本更新记录 | 小丁的个人博客](https://tding.top/archives/2bd6d82.html)

2. 参考了本篇博客的大部分内容 [hexo添加新菜单并实现新菜单的文章归类_weixin_30312557的博客-CSDN博客](https://blog.csdn.net/weixin_30312557/article/details/98233523?utm_medium=distribute.pc_relevant.none-task-blog-OPENSEARCH-6.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-OPENSEARCH-6.control)