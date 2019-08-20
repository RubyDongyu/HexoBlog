---
title: groovy
categories:
  - languages
tags:
  - languages
date: 2018-10-10 02:23:35
---

### 安装

通过sdkman(The Software Development Kit Manager)
>1.获取并设置环境
```
$ curl -s get.sdkman.io | bash
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```
>2.安装groovy
```
$ sdk install groovy
```

### HelloWorld
安装完成后就可以通过下面的命令运行第一个groovy程序
- 命令执行
```
dongyu@compiler52157:~$ groovy -e "println 'Hello World\n'"
```
输出内容如下
```
Hello World
```
- 文件执行
```groovy
public class HelloWorld {
    public static void main(def args) {
        println 'Hello World\n'
    }
```
```shell
$ groovy HelloWorld.groovy
```
- 字节码执行

```
```


###  运行时元编程
![image](http://docs.groovy-lang.org/latest/html/documentation/assets/img/GroovyInterceptions.png)