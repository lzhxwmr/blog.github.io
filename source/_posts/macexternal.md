---
title: MacBook Pro 外接显示器设置（高刷新率）
date: 2020-09-07 18:05:06
tags:
    - MacBook
    - macOS
    - 外接
    - 显示器
    - 高刷新率
categories:
    - 记录
---
>今天莫名把MacBook在外接显示器上面的刷新率提升到了144Hz，比较激动，于是记录一下
<!--more-->

## 设备
* MacBook Pro Mid 2017<span id="spoiler">虽然是2018年中买的</span>
* SAMSUNG C27JG5x

详细信息如图
![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/09/08/d1051a.png)
![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/09/08/aac520.png)

## 提要
其实很显然的是，如果想要达到144Hz的刷新率有这么几个方面需要考虑：
1. 显示器支持高刷新率
2. 显卡支持高刷新率（似乎2014的mbp都能支持？）
3. 线材支持高刷新率或者说<span id="inline-green">高传输能力</span>
4. 如果像我一样是2016以后的model，则要注意转接头（adapter）的传输能力

### 显示器支持
这个不需多说，大家懂得都懂，不懂的大概率不会点进来。<span id="spoiler">真的不懂的话可以评论区提出来，我再补充说明</span>

### 显卡支持
这方面也不用多提，大多数MacBook Pro都有这样的能力。

### 线材支持
这方面和下一点转接头的支持一起作为常见的限制瓶颈，都是我们今天讨论的重头戏。

目前就我的显示器而言，可以支持的接口的DP和HDMI两种，经过笔者测试，在RTX 2060上得到的结果是HDMI能够支持到120Hz而DP可以支持144Hz。

但是之前笔者通过DTK使用显示器附赠的线材（HDMI）连接显示器发现，可以支持到120Hz的刷新率。而与之相比，我的MBP使用官方的转接头连接到该显示器只能支持到60Hz并且不能更改刷新率。所以笔者动手去查证了一下官方的转接头的视频输出能力：

[![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/09/08/e2f883.png)](https://www.apple.com/shop/product/MUF82AM/A/usb-c-digital-av-multiport-adapter)

于是恍然大悟。然后笔者光速下单Amazon上随便挑了一款adpter，今天就换上试了一下。

结果还是没用？\
然后笔者发现了因为是用的switch附赠的那条HDMI连接的显示器，这个时候线材成为了瓶颈（因为switch的TV模式输出最高依旧是1080p 60Hz）。

所以笔者的经历告诉大家，在实施高刷新率计划的时候，需要满足线材的支持。但是笔者的情况比较特殊，目前使用的显示器仅仅是2K@144Hz，而目前市面上能够买到的线材主要能够支持的最高分辨率x刷新率是4K@60Hz。所以如果显示器是4K并且希望输出刷新率144Hz，那么HDMI的方案大概率是行不通的，此时应该更换DP接口的线材。

另外，type c转换HDMI/DP线材也是一个很好的选择，可以省去转换器的烦恼，但是选购的时候依旧要重点关注线材的传输能力。

### 转换器支持
作者在上文中已经使用亲身经历说明了转换器作为瓶颈可能发生的问题，至少可以确定的是苹果官方那一款肯定是不支持高刷新率了，如果同样有使用这一款的想要有所改观可以换购其他的试试。

## 小结
所以上述已经基本把视频传输的几个瓶颈都概括出来了。毕竟视频信号传输的路径也就是\
MacBook Pro(Graphic Card) -- (Adapter) -- Cable -- Monitor\
自己排除问题的时候也可以根据这种模型来判断一下再进行相关搜索。

如果大家还有什么疑惑或者建议欢迎在评论区留言分享。

最后上一张成果图
![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/09/08/5e69da.png)