---
title: Worth(DTK rental) > (500 - 200)USD?
date: 2021-02-04 11:48:05
tags:
	- 吐槽
	- Apple silicon
	- Universal App Startup Kit
	- Developer Transition Kit
	- Mac Mini
	- ARM
	- A12Z Bionic
	- 苹果
	- Apple Developer
categories:
	- 吐槽
	- 日志
---

> 在体验了大半年的 DTK 之后，终于收到了来自苹果的退还通知邮件。

<!-- more -->

_文章著作权归 zhli.me 所有，转载请注明出处_

## 邮件正文

![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/img/20210204135922.png)
这封邮件的大致内容就是说：

> 感谢您使用 DTK。\
> 由于现在我们已经推出了搭载 M1 处理器的 MBA，Mac Mini 以及 MBP，我们即将回收您手上的 DTK。\
> 感谢您参与本项目，为了表达感谢，我们将在确认收到 DTK 之后给您提供价值 200 USD 的优惠券，供您用来购买搭载了 M1 的 Mac 设备。在您的一年项目时间结束前，您仍然可以访问该项目(Universal App Quick Start Program)的其他资源，例如技术支持以及私有的讨论论坛。

其实读完邮件后，笔者第一感觉是，苹果在用 500 <span id="inline-green">USD</span> 的价格出租了 DTK 之后，现在即将收回机器，并且给到每个租用机器的开发者 200 <span id="inline-green">USD</span> 的额度补偿。看起来可以说是十分 _“慷慨”_ 了。

**然而事情真的是这样吗？**

## 重点<span id="spoiler">列文虎克</span>

笔者看完邮件后思来想去觉得很不对劲，于是又反复仔细阅读了一下，发现了一些<span id="inline-red">“重点”</span>

### 优惠券购买限制

邮件中提到
![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/img/20210204135924.png)

> 我们将在确认收到 DTK 之后给您提供价值 200 USD 的优惠券，**供您用来购买搭载了 M1 的 Mac 设备**

也就是说该优惠券仅供购买 M1 设备使用。

### 优惠券时间限制

邮件中还有很小的一行注释
![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/img/20210204135923.png)

> 该优惠券有效期截止于 2021.5.31

## 分析

其实将上述的两个重点联系起来，可以说是苹果逼着这些已经租用过 DTK 的开发者再去购买一台 M1 Mac 了。而且从另一个角度来看，<span id="inline-blue">May 31, 2021</span> 这个日期也是十分尴尬的，因为以往经验来说，苹果的<span id="inline-purple">WWDC</span>会在六月份举行，届时会发售新的产品。而根据网上的流言，这次有可能会发售新的 MBP。
![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/img/20210204143140.jpg)
如果这张图的真实性可以得到确认，那么 WWDC 上很有可能会宣布一款搭载 M2 处理器的新 Mac，而 DTK 给到开发者的优惠券将无缘这些产品。

分析到这里，只能说苹果的销售策略太“高明”了。

首先是 DTK 所搭载的 [A12Z Bionic](https://zh.wikipedia.org/wiki/Apple_A12Z) 处理器，能够完美地消化 2020 的 iPad 搭载的 [A12X Bionic](https://zh.wikipedia.org/wiki/Apple_A12X_Bionic) 的库存。

其次是，在搭载 M2 芯片的 Mac 发售前，将现有的 M1 Mac 库存通过这一个优惠码刺激消费从而处理掉。

## 小结

笔者从个人的角度出发，觉得这次苹果的做法不太妥当。

首先就 DTK 本身的表现而言，这款机器可以说基本没有太多的官方支持。其运行的 Big Sur Beta 在一天之中可以引发无数的 kernel panic，导致笔者拿到机器后根本没有办法正常运行任何测试——因为测试刚刚开始机器就重启了。而根据论坛上先有的信息，非常多的开发者也面临着这些问题。所以就苹果所提供的关于 DTK 的服务来说，是远远值不上这个<span id="inline-green">500-200 = 300 USD</span>的价值的。

而考虑到现实情况，其实真正单一地靠开发 iOS 应用谋生的独立开发者并不多，其中营收较高的独立开发者更是凤毛麟角。所以申请了该项目，并且通过该项目保证了应用在新平台上正常运行的开发者之中，从项目中获益超过付出的人不会是大多数。

笔者也在浏览 Reddit 论坛的时候发现了相似的观点：

![](https://cdn.jsdelivr.net/gh/gitosun/yedetuku/img/20210204135921.png)

> 那些觉得有 200 美元优惠券很值得的人，多半是站在类似 Adobe 和 MS 的大公司的角度上看待的这个问题。并非每一个为新平台开发共享的开发者都是从属于这些大公司的，尤其是那些会想办法让自己的项目在 DTK 上成功运行并开源分享的人们，他们从中连一毛钱都赚不到。

而笔者作为一个无法从这个项目乃至苹果平台开发中直接获利的开发者，同样对此感到沮丧。虽然在申请项目的时候已经做好了什么都不会得到的心理准备，可是未曾想到为新平台所付出的时间和精力，到了最后却还不得不通过付出更多的钱来止损。也许留下这$500，拿去买$649 的 M1 Mac Mini 更为值得吧，至少后者不会出现 kernel panic 频繁到无法运行测试的地步。

从营销的角度来看，DTK 与其说是一个技术过渡项目，更多还是一个销售项目，不仅让库存中的 A12X 发光发热，还推进了 M1 设备的销售，可以说是“双赢”了。

**可是代价是什么呢？**
