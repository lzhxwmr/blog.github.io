---
title: 通过Github Pages搭建Hexo（二）
date: 2020-02-04 02:34:58
tags:
	- 教程
	- hexo
	- gitpages
	- 博客
	- 记录
	- 主题自定义
	- Theme customization
categories:
	- 教程
	- 记录
---
>这一篇主要是对主题一些小的细节的自定义的记录以及一些功能的添加
<!-- more -->
# 主题自定义
笔者在完成了Hexo博客的基本搭建后，从各个方面上面探索和完善了博客（让他有一个博客应该有的样子）
## 启用评论功能(Disqus vs Valine)
可以启用的评论功能有很多，在theme/next下的<span id="inline-green">_config.yml</span>里面我们可以看到有很多comment的选项：
```
# Available values: changyan | disqus | disqusjs | gitalk | livere | valine
```
笔者目前尝试过的评论系统则是disqus和valine两个。
因为使用时间不够长（没有用户），所以只能够说说大家的看法和个人看法。
### 使用体验
Disqus似乎最大的缺点在于墙内无法访问，而Valine是基于Leancloud部署，因此其打开速度相对来说好很多。
### 部署步骤
#### Disqus的部署
1. 去Disqus注册一个账号，新建一个应用（评论）
2. 在theme/next下编辑<span id="inline-green">_config.yml</span>
   找到disuqs字段，修改enable为true，然后将Disqus上注册的应用的id填到shortname上
```
disqus:
  enable: true
  shortname: your_id
```
#### Valine的部署
1. 注册Leancloud账号，然后新建一个应用
2. 将应用keys里面的AppID和AppKey拷贝到theme/next下编辑<span id="inline-green">_config.yml</span>的字段中
   字段修改如下
```
valine:
  enable: true
  appid: yoru_app_id
  appkey: your_app_key
```
## 自定义头像（Avatar）
这是一个很简单的事情，总的来说就是
- 找到想要的头像
- 修改并且minify一下（推荐使用tinypng）
- 上传到图床得到url（二选一）
- 放到theme的source文件夹下的新建uploads文件夹（也可以是别的文件夹但是后面的设计就需要更改）（二选一）
- 修改theme/next下<span id="inline-green">_config.yml</span>的avatar:
```
avatar:
  url: 图床url 
  或者
  url: /uploads/avatar.png
```
## 背景动画(Canvas Nest)
本博客现在展示的背景动画效果就是由canvas nest实现的。
这是一个在NexT主题中默认就有的选项。但是问题在于并不是直接在them/next下的<span id="inline-green">_config.yml</span>中enable就能够直接使用的。除了修改<span id="inline-green">_config.yml</span>外还有一些操作要做。
具体的说明在[GitHub](https://github.com/theme-next/theme-next-canvas-nest)上面有讲
在此就简略说明一下：
1. 修改<span id="inline-green">_config.yml</span>的canvas_nest字段：
```
canvas_nest:
	enable: true
```
2. 进入next主题目录，git clone项目
```
cd themes/next
git clone https://github.com/theme-next/theme-next-canvas-nest source/lib/canvas-nest
```

至此基本的优化/美化就完成了，下一篇可能会对这一篇还没有cover到的方面进一步说明。
（也许日后能够成为博客炸了再次搭建的备份）