---
title: 更新Hexo以及NexT主题
date: 2020-08-25 15:18:09
tags:
    - 更新
    - 升级
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
> 一次大版本升级历程
<!-- more -->
截至目前，在github上维护的<span id="blue">NexT</span>主题有三个不同的仓库：

|版本|年份|仓库|
|-|-|-|
|v5.1.4 或更低|2014~2017|https://github.com/iissnan/hexo-theme-next|
|v6.0.0 ~ v7.8.0|2018 ~ 2019|https://github.com/theme-next/hexo-theme-next
|v8.0.0 或更高|2020|https://github.com/next-theme/hexo-theme-next|

笔者升级的动力在于自定义一些fontawesome的时候发现新版本的不受支持，因此萌生了升级的想法。

# 环境
* Hexo v4.0
* NexT v7.1

本次升级的目标版本是NexT v8.0.0。

# 更新Hexo
更新Hexo的方式也就是更新npm包的方式，最简单的就是`npm update -g hexo`。
但是除此之外笔者也在网络上找到了其他的方法，也就是使用npm-check检查更新，然后使用npm-upgrade进行更新:
```shell
npm i -g npm-check npm-upgrade
npm-check
npm-upgrade
```
在更新完之后可以通过`hexo version`命令来验证更新。

# 更新NexT
## 备份原有主题
这一点其实是确保新的<span id="blue">NexT</span>主题不会覆盖旧的主题，所以备份可以通过两种方式实现
1. 将原有的<span id="blue">NexT</span>主题文件夹重命名为next以外的名称
2. 在git clone的时候将新的<span id="blue">NexT</span>主题clone到next-reloaded里面

笔者这里选择了第二种方式。

## 下载新版本
首先进入hexo的工作目录再进行操作
```shell
# cd hexo-site
git clone https://github.com/next-theme/hexo-theme-next themes/next-reloaded
```
然后通过对比新老`_config.yml`来进行新的主题的配置。同时，如果之前对样式有自定义修改的话，也需要同步修改到新的主题里面。

## 配置的变化
因为`_config.yml`的配置与老版本大同小异，所以这边不过多赘述，只挑出笔者觉得值得一提/记录的内容写写。
1. 动画效果从`Velocity.js`修改为了`Animate.css`
2. CDN的配置更加方便，不需要在vendors里面再去修改各个依赖的CDN地址，直接在最上方选择修改CDN提供商即可
3. 更新了fontawesome的版本，能够使用新的图标
4. 自定义文件的名称变更，旧版本的`.swig`文件变为`.njk`
5. 代码块的高亮主题可以跟随dark mode更换

## Tip
除了上述值得注意的变化，还有一些需要注意的地方

### pace
因为`pace.js`太久没有更新，已经被认定为失效，因此在将来的版本中可能会使用`nprogress`来代替。

但是笔者发现现在还是能够继续使用，只是在配置上需要手动配置其对应主题的css的cdn，否则样式不会随设置而改变。
也就是在上面的pace字段里面修改了主题样式之后，需要在vendor字段也设置对应的cdn地址。

例如本blog的pace主题是flash，那么对应的两个字段的配置如下：
```yml
pace:
  enable: true
  # Themes list:
  # big-counter | bounce | barber-shop | center-atom | center-circle | center-radar | center-simple
  # corner-indicator | fill-left | flat-top | flash | loading-bar | mac-osx | material | minimal
  theme: flash


vendors:
  ...
  # Pace.js
  pace:
  pace_css: https://cdn.jsdelivr.net/npm/pace-js@1.0.2/themes/blue/pace-theme-flash.css
```

### Canvas Nest
[theme-next-canvas-nest](https://github.com/theme-next/theme-next-canvas-nest)的配置发生了改变，从前是放在`_config.yml`中，但是现在是放到了foot里面。

具体在笔者的例子里面就是在`footer.njk`中加入
```html
<script color="0,0,255" opacity="0.5" zIndex="-1" count="99" src="https://cdn.jsdelivr.net/npm/canvas-nest.js@1/dist/canvas-nest.js"></script>
```

# 小结<span id="spoiler">吐槽</span>
配置好这些东西花了笔者一个下午。总结下来遇到的最大的麻烦是三个主题仓库，让笔者一开始配置了很久的v7.8.0，之后又不得不重新配置v8.0.0。

这一次错误配置的感受是，自定义配置样式文件与主题目录分离真的是太好了<span id="spoiler">，有效避免了笔者又去配置一次样式</span>。

下一篇有关内容可能会在把样式配置得更满意之后，记录一下个人样式配置心得。

># 参考链接
>* https://github.com/next-theme/hexo-theme-next/issues/4
>* https://github.com/next-theme/hexo-theme-next/issues/3
>* https://whjkm.github.io/2018/07/17/Hexo%E7%89%88%E6%9C%AC%E5%8D%87%E7%BA%A7%E5%92%8CNext%E4%B8%BB%E9%A2%98%E5%8D%87%E7%BA%A7%E4%B9%8B%E5%9D%91/
>* https://github.com/theme-next/theme-next-canvas-nest