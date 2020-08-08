---
title: DTK Mac Mini上手兼容性记录
date: 2020-08-03 00:45:14
tags:
	- Apple silicon	
	- Universal App Startup Kit
	- Developer Transition Kit
	- Mac Mini
	- ARM
	- A12Z
	- 苹果
categories:
	- 记录
	- 日志
---

**最近搬家完毕，也终于有空开箱DTK了。不过为了尊重本来就没啥用的保密协议，这里就只放上一张开箱图**

<!-- more -->

## 实机图片

![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/08/03/9195a3.png)

![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/08/03/5d7981.png)



**为了方便称呼，这台采用了A12Z核心的Mac Mini下面统统用<span id="inline-green">dtk</span>代替。**

## 配置

如上述的系统信息以及网上放出的消息我们可以知道<span id="inline-green">dtk</span>的配置如下

* CPU: Apple A12Z Bionic
* 内存: 16GB
* 硬盘: 512GB(SSD)



## 使用感受

本来笔者想把这台机器作为一个家用台式的角色使用，但是这一方面该机器未能达标。

### 输入卡顿

注意这里是输入卡顿而不仅仅是输入法卡顿。虽然可能的原因各种各样，但是目前输入卡顿最严重的地方就在于Safari的搜索栏，在这里成功体现了不仅仅是中文输入法卡顿，与此同时就算只是键入英文也会卡顿。如果排除掉我的键盘没电的问题，可能是这一块的Autocomplete的问题。

### 大多数软件不兼容

其实这一点比较个人化一点，因为我想用的desktop程序都不兼容，因此我会给一个不兼容的评价。但是，谁会去拿<span id="inline-green">dtk</span>是为了跑之前已经写在x86_64平台上面的程序呢🤷‍♂️？（🙋‍♂️笔者）

所以抛开原有未修改的x86_64平台的程序的部分，我们通过开发者提前修改程序以适应新平台的角度来看，这个<span id="inline-green">dtk</span>简直是惊艳。很多iOS上面的app都可以安装到Big Sur上面运行。至于各种语言运行环境……可能是笔者太笨还没找到Rosetta 2的使用方法吧。

## 兼容性清单

### ✅Telegram

来源： 官网下载

可用性： 官网有提供两个版本，一个是desktop版，另一个是for Mac版本。两者中后者是手机app的移植，流畅正常运行，不过笔者无法适应那种UI布局。而前者则原本是x86_64的程序，在<span id="inline-green">dtk</span>上的兼容性尚可，不过经常出现网络通信时间过久的问题，笔者略微怀疑是网络有问题（非<span id="inline-green">dtk</span>的原因）。



### ❌Spotify

来源： 官网下载

可用性： 不可用



### ✅Spark

来源： MAS

可用性： 可用



### ✅Manico

来源： MAS

可用性： 可用



### ❌Chrome

来源： 官网

可用性： 不可用。直接启动就是崩溃，这在Safari的表现暂时还不很稳定的前提下，直接让笔者放弃了用<span id="inline-green">dtk</span>作为主力台式的想法。



### ✅iTerm 2

来源： 官网

可用性： 可用



### ✅Typora

来源： 官网

可用性： 可用



### ❌Notion

来源： 官网

可用性： 不可用。点击后显示Notion已启动但是没有窗口弹出。



## 工具兼容性

### ⭕Homebrew

来源： 官网

可用性： 可用。但是需要一点点workaround和额外操作：https://github.com/Homebrew/brew/issues/7857#issuecomment-652614544



### ✅htop

来源： brew

可用性： 可用。



### ✅git

来源： Xcode（自带）

可用性： 可用。但是需要先输入`sudo xcodebuild -license`来同意license。



### ✅NodeJS

来源： brew

可用性： 可用



### ✅ Scroll Reverser

来源： 官网

可用性： 可用。可以暂时替代Logitech Options调整鼠标滚动方向。



## 小结

总的来说<span id="inline-green">dtk</span>名副其实，主要就是一个供开发者过渡使用，将自己原有的iOS的app移植到新的Apple Silicon平台以及将旧的x86_64平台的程序移植到新平台上，使得之后Big Sur以及新的ARM MacBook发售的时候有足够的应用生态以及完整的开发工具链来支撑其销量。

不过笔者还是觉得在接下来两年内还是x86当道的，同时也让我们静静观望Apple Silicon能够给苹果全家桶带来怎样的改变。

（不过能够拿着一个没屏幕的16G内存512G大容量的iPad Pro真爽←误）



**参考链接** ： https://lscho.com/tech/dtk.html