---
title: 在树莓派上安装Samba 4.12
date: 2020-09-08 21:41:13
tags:
    - 树莓派
    - raspberry
    - pi
    - samba
    - Time Machine
categories:
    - 记录
    - 折腾
---
>最近因为想把Time Machine给转到树莓派4B+上，所以折腾了一番Samba相关的东西，这里讲讲自己编译安装Samba 4.12的过程。<span id="spoiler">主要是真的找不到类似的自己编译的记录于是自己写一下</span>
<!--more-->
# 准备工作
笔者这里使用的硬件是树莓派4B+，系统是官方的Raspbian（也就是Debian 10）
首先要安装需要的[包](https://wiki.samba.org/index.php/Package_Dependencies_Required_to_Build_Samba)：
```shell
$ apt-get install acl attr autoconf bind9utils bison build-essential \
  debhelper dnsutils docbook-xml docbook-xsl flex gdb libjansson-dev krb5-user \
  libacl1-dev libaio-dev libarchive-dev libattr1-dev libblkid-dev libbsd-dev \
  libcap-dev libcups2-dev libgnutls28-dev libgpgme-dev libjson-perl \
  libldap2-dev libncurses5-dev libpam0g-dev libparse-yapp-perl \
  libpopt-dev libreadline-dev nettle-dev perl perl-modules pkg-config \
  python-all-dev python-crypto python-dbg python-dev python-dnspython \
  python3-dnspython python-gpgme python3-gpgme python-markdown python3-markdown \
  python3-dev xsltproc zlib1g-dev liblmdb-dev lmdb-utils
```
# 下载
去[官网](https://www.samba.org/)下载最新稳定版本(stable)的samba源码
```shell
$ wget https://download.samba.org/pub/samba/stable/samba-4.12.6.tar.gz
$ tar -zxf samba-4.12.6.tar.gz
$ cd samba-4.12.6
```
# 编译
然后开始经典的编译安装环节
```shell
$ ./configure
```
如果上述依赖包都安装好了的话，此时应该是提示configure成功的。如果有说缺少什么包的话可以考虑检查是不是没有安装前置依赖或者也可以搜索排错一下。\
但是在这里作者停了一下，因为本身就安装有4.9.5版本的samba，所以安装前最好把原有的samba给卸载掉
```shell
$ apt-get remove samba samba-common -y
```
这边我们修改一下目标路径（不然的话就得手动修改PATH了）
```shell
$ ./configure --bindir=/usr/local/bin --sbindir=/usr/local/sbin/ --sysconfdir=/etc/samba/ --mandir=/usr/local/share/man/ --with-systemd
```
设置完成后就是进行编译，介于树莓派是4线程的，我们加上`-j 4`
```shell
$ make -j 4
```
不过如果发生报错了的话还是去掉多加的参数，老老实实地make排错吧。\
然后安装到指定的位置
```shell
$ sudo make install
```
# 测试
```shell
$ smbd -V
Version 4.12.6
```
# 小结
这里顺便贴一下samba/smb.conf的配置来备份一下
```conf
[TM]
comment=TM mount
path=/path/to/TM  # modify this line
browsable=Yes
writeable=Yes
only guest=no
create mask=0777
directory mask=0777
public=no
valid users = your user # modify this line
vfs objects = catia fruit streams_xattr
fruit:appl = yes
fruit:metadata = stream
fruit:time machine = yes
fruit:posix_rename = yes
fruit:veto_appledouble = no
fruit:wipe_intentionally_left_blank_rfork = yes
fruit:delete_empty_adfiles = yes
```
<span id="spoiler">但是Time Machine的备份速度丝毫不加快……阿西吧</span>
> 参考链接
>1. https://wiki.samba.org/index.php/Build_Samba_from_Source
>2. https://wiki.samba.org/index.php/Package_Dependencies_Required_to_Build_Samba