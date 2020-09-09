---
title: Java多版本安装管理（一）
date: 2020-08-13 15:39:44
tags:
    - Java
    - Multi Version
    - MacOS
    - Visual Studio Code
categories:
    - 记录
    - 日志
    - 教程
---
> 自从VS Code更新了之后，Java方面使用Eclipse功能的插件需求JDK 11+来使用了。这里记录一下多版本Java管理。

<!-- more -->

## 现有的环境

现有的环境有<span id="inline-blue">JDK8</span>。现在需要完成的事情就是安装上<span id="inline-green">JDK11</span>并且配置好多版本管理。
通过`java -version`可以看到现在的版本

```shell
$ java -version
java version "1.8.0_231"
Java(TM) SE Runtime Environment (build 1.8.0_231-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.231-b11, mixed mode)
```

## 管理选择
接下来在macOS上面可以选择的方案主要有两个：
* Homebrew
* jenv

因为前者几乎就是开发用的Mac的标配，所以笔者决定结合Homebrew来管理多版本环境。

## 操作过程
### 安装Homebrew
这一步<span id="spoiler">~~纯属水文章长度~~</span>用来提醒看教程的读者先去装好Homebrew环境。

官网上有详细的教程:[🔗链接](https://brew.sh)
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### 使用 brew cask
如果是第一次使用brew cask的话可以先在命令行中输入`brew tap homebrew/cask-versions`。

### 1. 如果想要安装最新版本的java
```shell
$ brew cask install java
```
### 2. 如果需要安装其他指定版本的java
```shell
$ brew tap homebrew/cask-versions
$ brew cask install java11
```
### 3. 查看安装好的Java路径
```shell
$ /usr/libexec/java_home -V
Matching Java Virtual Machines (2):
    11.0.2, x86_64:	"OpenJDK 11.0.2"	/Library/Java/JavaVirtualMachines/openjdk-11.0.2.jdk/Contents/Home
    1.8.0_231, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home

/Library/Java/JavaVirtualMachines/openjdk-11.0.2.jdk/Contents/Home
```
可以看出当前机器上同时有<span id="inline-blue">JDK8</span>和<span id="inline-green">JDK11</span>。而且现在系统路径中得到的java是11。

### 4.切换版本
虽然我们的默认版本已经切换到<span id="inline-green">JDK11</span>，但是众所周知其实很多应用还是无法运行在高版本的JDK下的<span id="spoiler">~~如MineCraft~~</span>，而且笔者的所有程序基本都是在<span id="inline-blue">JDK8</span>下调试运行的，因此还是需要把JDK切换回来<span id="spoiler">如果不是因为VS Code谁想装11</span>。

目前的切换解决方案主要是修改`$JAVA_HOME`环境变量，可以手动修改或者写好命令来切换环境。

在对应shell的文件里面修改(bash: ~/.bash_profile, zsh: ~/.zshrc)
```shell
# JDK 8
export JAVA_8_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home"
# JDK 11
export JAVA_11_HOME="/Library/Java/JavaVirtualMachines/openjdk-11.0.2.jdk/Contents/Home"

# 默认JDK8
export JAVA_HOME=$JAVA_8_HOME

# 命令别名切换版本
alias jdk8="export JAVA_HOME=$JAVA_8_HOME"
alias jdk11="export JAVA_HOME=$JAVA_11_HOME"
```
然后通过source来更新当前环境变量或者退出当前会话重新开启shell窗口:
```shell
# if bash
$ source ~/.bash_profile
# if zsh
$ soruce ~/.zshrc
```
### 5.测试
同时这也是上述命令使用方法
```shell
# 默认版本
$ java -version
java version "1.8.0_231"
Java(TM) SE Runtime Environment (build 1.8.0_231-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.231-b11, mixed mode)

# 切换至JDK11
$ jdk11
$ java -version
openjdk version "11.0.2" 2019-01-15
OpenJDK Runtime Environment 18.9 (build 11.0.2+9)
OpenJDK 64-Bit Server VM 18.9 (build 11.0.2+9, mixed mode)

# 切换至JDK8
$ jdk8
$ java -version
java version "1.8.0_231"
Java(TM) SE Runtime Environment (build 1.8.0_231-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.231-b11, mixed mode)
```
### 6.修改VS Code的java.home
在vscode中的settings.json中添加
```json
"java.home": "/Library/Java/JavaVirtualMachines/openjdk-11.0.2.jdk/Contents/Home"
```
即可。
<span id="spoiler">如果不是JDT/VS Code，谁又想折腾这种东西呢</span>

> 参考链接
>1. https://segmentfault.com/a/1190000013131276
>2. https://blog.csdn.net/qq_21808961/article/details/102256150