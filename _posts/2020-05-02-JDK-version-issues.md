---
title: 修改jdk版本问题，环境变量修改jdk版本无效，配置为jdk12却还是jdk1.8
author: 林叁柒
date: 2020-05-02 20:43:37 +0800
categories: [编程, JAVA, 使用JAVA所遇到的一些问题]
tags: [编程, JAVA, jdk, jdk版本问题]
---

## 导语：
原本使用jdk12版本，后来为了和基友们玩minecraft，就安装了jdk1.8，但是后来java -version的jdk版本为1.8而无法改为12
## 问题：
环境变量已修改为jdk12

![环境变量](/assets/img/sample/2020-05-02-JDK-version-issues/20200416152327481.png)

但在命令框输入java -version时为1.8版本

![命令框中显示的jdk版本](/assets/img/sample/2020-05-02-JDK-version-issues/20200416152432982.png)

根据网上的办法，需要删除以下的一些文件：
C:\ProgramData\Oracle\Java\javapath;
C:\Windows\System32目录下的三个java开头的.exe文件
然而我的电脑并没有这些文件
## 解决问题的过程：
然后我就详细地看了看配置环境变量的信息，然后就在Path中找到了这个：

![在这里插入图片描述](/assets/img/sample/2020-05-02-JDK-version-issues/20200416153137796.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwNjY4MTIx,size_16,color_FFFFFF,t_70)

如第一条环境变量所示：C:\Program Files (x86)\Common Files\Oracle\Java\javapath;
然后我就到这个文件夹看了看，正是网上说的要删除的几个文件：
![在这里插入图片描述](/assets/img/sample/2020-05-02-JDK-version-issues/20200416153322666.png)
## 解决方法：
因为jdk1.8安装时会自动配置一个环境变量在path里并置顶了，所以只需要把自己配置的jdk12的环境变量上移到jdk1.8自动配置的环境变量之前即可
也可以删除jdk1.8自动配置的环境变量

![在这里插入图片描述](/assets/img/sample/2020-05-02-JDK-version-issues/2020041615365575.png)