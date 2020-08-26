---
title: Srmd-ncnn-vulkan 编译记录
date: 2020-02-21 12:22:12
tags:
    - ncnn
    - nihui大佬
    - tencent/ncnn
    - vulkan
    - protobuf
    - vs
    - Visual Studio
categories:
    - 记录
    - 编译
---
>nihui大佬！！！
<!-- more -->
[推特膜拜入口](https://twitter.com/nihui/status/1230117266747875328?s=20)

偶尔在推上看到了nihui大佬挖的新坑，可以将图片放大并降噪，而最近拍的照片像素不太够作为壁纸的时候自动缩放总是会导致马赛克频出，因此想要尝试使用srmd来放大一下拍出来的壁纸。

## 编译环境

* Windows 10 1909
* Visual Studio 2019
注：VS一定要在开始前装好，并确认C++相关组件已安装

## 编译protobuf

打开Visual Studio Tools下的x64 Native Tools Command Prompt for VS 2019
下载<span id="inline-blue">protobuf</span>并解压：https://github.com/google/protobuf/archive/v3.4.0.zip

```shell
cd <protobuf-root-dir>
mkdir build-vs
cd build-vs
cmake -G"NMake Makefiles" -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=%cd%/install -Dprotobuf_BUILD_TESTS=OFF -Dprotobuf_MSVC_STATIC_RUNTIME=OFF ../cmake
nmake
nmake install
```

其中需要强调的是，mkdir了之后不要忘记进入目录，不然后面的cmake找不到CMakeLists（~~只有笔者才会犯的错误~~）

## 编译ncnn

### 安装Vulkan SDK

因为下面的项目用到了<span id="inline-yellow">Vulkan</span>，因此现在必须先安装好<span id="inline-yellow">Vulkan SDK</span>：https://vulkan.lunarg.com/sdk/home
并且设置好环境变量。
需要设置的环境变量分别是：

1. Vulkan_INCLUDE_DIR: %VULKAN_SDK%\Include
2. Vulkan_LIBRARY: %VULKAN_SDK%\Lib
3. VULKAN_SDK: path-to-vulkan

<center><img src="https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/04/16/e66c30.png" width=50%></img></center>

其中VULKAN_SDK是安装好就自动设置好了的，只需配置1、2即可。

### 编译ncnn库

依旧是打开我们心爱的x64 Native Tools Command Prompt for VS 2019

```shell
git clone https://github.com/Tencent/ncnn.git
cd <ncnn-root-dir>
mkdir -p build-vs
cd build-vs

# 其中的<protobuf-root-dir>请自行替换
cmake -G"NMake Makefiles" -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=%cd%/install -DProtobuf_INCLUDE_DIR=<protobuf-root-dir>/build-vs/install/include -DProtobuf_LIBRARIES=<protobuf-root-dir>/build-vs2017/install/lib/libprotobuf.lib -DProtobuf_PROTOC_EXECUTABLE=<protobuf-root-dir>/build-vs/install/bin/protoc.exe -DNCNN_VULKAN=ON ..

nmake
nmake install
```

至此<span id="inline-purple">ncnn</span>的库基本就编译好了。如果遇到了编译错误可以从路径、之前的编译、以及上述的各个配置入手排除。应该是没什么bug或者错误的。

## 编译srmd-ncnn-vulkan

项目最终使用VS 2019编译完成。

### 生成项目

```shell
git clone https://github.com/nihui/srmd-ncnn-vulkan.git
cd srmd-ncnn-vulkan
```

现在我们来修改src中的CMakeLists.txt文件。
找到文件中如下内容

```shell
# change these path to yours
set(ncnn_DIR "/home/nihui/dev/ncnn/build/install/lib/cmake/ncnn")
```

将set后面的`/home/nihui/dev/ncnn/build/install/lib/cmake/ncnn`设置为刚刚ncnn编译好后install中的对应路径。
在刚刚的编译中应该得到的路径就是`<ncnn-root-dir>/build-vs/install/lib/cmake/ncnn`
记得要把win路径中的<span id="inline-red">\\</span>替换为<span id="inline-green">/</span>。
然后我们在srmd-ncnn-vulkan中继续命令行：

```shell
cd src
mkdir build
cmake -B build\
```

这时在build文件夹下就生成了srmd的sln，接下来就可以使用vs来编译生成exe了。

### 编译exe

打开`build/srmd-ncnn-vulkan.sln`
将solution configuration中的Debug修改为Release

<center><img src="https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/04/16/a81295.png" width=50%></img></center>

然后右键srmd-ncnn-vulkan进行编译。

<center><img src="https://cdn.jsdelivr.net/gh/gitosun/yedetuku/2020/04/16/c9789a.png" width=50%></img></center>

提示编译成功后即可在bulid目录下的Release中找到生成的exe

## 小结

你以为我给自己挖的坑现在就说完了？
NO NO NO
现在得到的exe文件并不能直接在当前目录下直接跑出github上给出的示例命令。原因就是示例命令中没有给出当前exe所处的工作目录，也没有-m来指定model的目录，因此直接在Release下运行会报错`_wfopen() ??? failed`。想要解决这个问题有两种方法：

1. 通过-m指定model目录
2. 如果想用项目自带的model，将srmd-ncnn-vulkan.exe移动到`srmd-ncnn-vulkan/models/`下

然后就能够成功运行了(当然input.jpg自备)
试着作死用XPS的集显跑了一下，跑了十分钟才完成一张图，感觉整个电脑都起飞了。

感谢nihui大佬！

参考链接：

1. https://github.com/Tencent/ncnn/wiki/how-to-build#build-for-windows-x64-using-visual-studio-community-2017