---
title: java命令执行时，报Error：A JNI error has occurred, please check your installation and try again
author: 林叁柒
date: 2020-05-02 23:30:04 +0800
categories: [编程, JAVA, 使用JAVA所遇到的一些问题]
tags: [编程, JAVA, jdk, jdk版本问题, 报错]
---

## 导语：
我本来是使用jdk12版本来学习java的，而前几天为了和基友们玩minecraft，就安装了jdk1.8，本来在开发软件中敲代码运行是没问题的，后来心血来潮使用命令框运行就出现问题了
## 错误信息：
用命令框执行.class文件时，报错，错误信息如下：

![异常描述](/assets/img/sample/2020-05-02-Error-A-JNI-error-has-occurred/20200416150215990.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwNjY4MTIx,size_16,color_FFFFFF,t_70)

## 翻译后的意思：

![在这里插入图片描述](/assets/img/sample/2020-05-02-Error-A-JNI-error-has-occurred/2020041615043675.png)

## 原因：
也就是说，该文件是由高版本编译的，而执行是低版本执行的。
可以用java -version和javac -version查看运行和编译的版本信息。

![在这里插入图片描述](/assets/img/sample/2020-05-02-Error-A-JNI-error-has-occurred/20200416151211965.png)

## 解决办法：
更改jdk或者jre版本即可
## jdk版本修改方法：
去修改环境变量即可
配置时可能会遇到的一些问题之一可参考：[修改jdk版本问题，环境变量修改jdk版本无效，配置为jdk12却还是jdk1.8](/posts/JDK-version-issues/).
