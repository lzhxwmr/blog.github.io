---
title: 通过Github Pages搭建Hexo（一）
date: 2020-02-03 21:01:46
tags:
	- 教程
	- hexo
	- gitpages
	- 博客
	- 记录
	- 部署
categories:
	- 教程
	- 记录
---

用这个系列来记录一下这个博客搭建的心路历程。
<!-- more -->
# 工具选择
首先，我们可以选择的搭配方式多种多样。

博客方面可以选择Hexo、Wordpress等，部署环境更是多种多样，从独立服务器（Dedicated Server）、VPS到Docker、Heroku等虚拟容器都是很好的选择。

而选择Hexo作为日常用博客主要是因为其干净整洁并且轻量的整体布局。另一点关键原因则是Hexo的运作方式与Github的工作部署流程很类似，因此和让人觉得得心应手。虽然更成熟的博客框架如Wordpress能够提供更多的特性和插件，但是个人使用起来觉得WP提供的各种各样的插件在用不到的时候会成为很大的累赘。并且WP对部属环境的需求较Hexo而言更高一些，可以说很多新手在初入门的时候，搭建WP遇到的最大的问题就是搭建和配置LNMP/LAMP环境。虽然搭建好的Wordpress十分适合用户使用，但是搭建的这个过程的痛苦笔者实在不想再次经历了。于是为了让自己轻松一点，又接着GitHub Education的契机，笔者选择了GitHub Pages作为承载Hexo的环境。

# 准备工作
- 如果没有GitHub账号的话，注册一个
- 在当前使用的设备上应该具备的环境要求：
	- Node.js 
	- Npm
	- Git

# 正式部署
## GitHub上的操作
### 1. 创建仓库
创建一个新的repository,命名为`(项目名).github.io`。此时GitHub不会自动将该仓库设为GitHub Pages。如果填写项目名为用户名会被自动设为GitHub Pagegs，会与我们后面的设置冲突。
### 2. 建立分支
这一部分可以根据各自的需求和习惯进行项目的分支管理。
笔者为了避免采用GitHub和Hexo两者互相干涉，所以将master分支空置，使用gh-pages来进行hexo deploy。
## 本地操作
### 1. 安装Hexo
```
npm install -g hexo-cli
```
### 2. 初始化
```
hexo init blog
```
其中blog可以替换成任意的项目名字。如果留空的话会在当前的目录下直接初始化项目。
### 3. 新建分支
首先拉取GitHub master分支，然后通过checkout切换分支，之后push来初始化gh-pages分支。
```
git clone https://github.com/yourusername/yourprojectname.git(你的项目地址)
git checkout -b gh-pages
git push origin gh-pages
```
## GitHub Pages修改分支
进入项目主页，在`Settings -> Options -> Github Pages`中，将Source切换为gh-pages分支，然后Save，至此配置就基本完成了。

# Hexo的使用
Hexo的基本用法：
- 生成文件 hexo g(enerate)
- 清除文件 hexo clean
- 启动服务器（默认4000端口） hexo s(erver) -p 4000
- 部署 hexo d(eploy)

# Hexo的部署
现在我们离最终能够看到博客只有一步之遥了。
接下来我们需要做的就是更改项目根目录下的_config.yml文件来设置deploy的目标和部署到远端。

首先安装hexo的git工具，来到blog的根目录下：
```
npm install hexo-deployer-git
```

然后修改_config.yml：
```
deploy:
  type: git
  repo: git@github.com:yourusername/yourprojectname.git(你的项目地址)
  branch: gh-pages
```

最后在博客目录下执行部署：
```
hexo d
```

至此，整个博客的基本部署就已经完成了，现在打开gitpages的地址`(你的GitHub用户名).github.io`即可看到和本地（hexo s）一样的效果。

下一篇的内容将主要关于Hexo的基本设置、主题安装、自定义logo、博文创作等。


> 参考链接：https://sisibeloved.github.io/hexoBlog/2018/04/12/Github-Pages部署个人博客-Hexo篇/