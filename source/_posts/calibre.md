title: calibre
author: Ruby Dongyu
tags:
  - calibre
categories:
  - calibre
date: 2018-06-28 14:58:00
---
[开发者网站](https://manual.calibre-ebook.com/develop.html)

calibre是python开发的一站式电子书阅读器，通过阅读代码学习python。

#### 获取源码
```
git clone git://github.com/kovidgoyal/calibre.git
```

#### 编译
In order to bootstrap the raw git sources to a release-ready state, run the 
command::
```
python2 setup.py bootstrap
```
In order to compile the C/C++ extensions etc. for a release-ready tarball
(these functions are already included by the bootstrap function), run the 
commands::
```
python2 setup.py build
python2 setup.py gui
```
#### 安装
The first type of install will actually "install" calibre to your computer by
putting its files into the system in the following locations:

 - Binaries (actually python wrapper scripts) in <prefix>/bin
 - Python and C modules in <prefix>/lib/calibre
 - Resources like icons, etc. in <prefix>/share/calibre

This type of install can be run by the command::
```
sudo python2 setup.py install
```
<prefix> is normally the installation prefix of python, usually /usr.  It can
be controlled by the --prefix option.

For distro packagers, DESTDIR support is implemented via the --staging-root
option, usually ${DESTDIR}/usr.

#### 开发
This type of install is designed to let you run calibre from your home
directory, making it easy to hack on it.

It will only install binaries into /usr/bin, but all the actual code and
resource files will be read from the calibre source tree in your home directory
(or wherever you choose to put it).

This type of install can be run with the command::
```
sudo python2 setup.py develop
```
