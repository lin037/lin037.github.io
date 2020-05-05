---
title: springboot整合shiro项目，打开页面却在后台调用登录接口
author: 林叁柒
date: 2020-05-02 20:51:35 +0800
categories: [编程, JAVA]
tags: [编程, springboot, shiro, 框架, 使用Java遇到的一些问题]
---

## 导语
springboot+shiro整合的项目中，没啥问题的，当倒入前端页面时，运行项目打开页面会发现，页面会调用shiro的登录接口，但页面还是正常访问，并且静态资源也都已正确引入。
## 问题介绍
shiro中发现静态资源的部分代码：
```java
        map.put("/static/*","anon");
        map.put("/*.html","anon");
        map.put("/js/*","anon");
        map.put("/css/*","anon");
        map.put("/img/*","anon");
        map.put("/fonts/*","anon");
```
当我打开页面时，显示正常，但后台打印出调用了shiro的登录方法

![在这里插入图片描述](/assets/img/sample/2020-05-02-Springboot-integrates-the-shiro-project-and-invokes-the-login-interface/20200501192610556.png)
## 解决办法

其实是因为springboot中带有图标的请求（favicon.ico）即打开页面会发送/favicon.ico的请求，而shiro中并没有配置，所以才会调用登录方法，加上即可

```java
        map.put("/static/*","anon");
        map.put("/*.html","anon");
        map.put("/js/*","anon");
        map.put("/css/*","anon");
        map.put("/img/*","anon");
        map.put("/fonts/*","anon");
        map.put("/favicon.ico","anon");
```
不过以此代码，可能使用IE打开还是会调用，因为本人使用的是bootstrap框架，以此可能会请求css/static/...的资源，而/css/* 仅仅是放行css下一级目录，而并非所有子目录，所以应改为/css/**

```java
		map.put("/static/**","anon");
        map.put("/*.html","anon");
        map.put("/js/**","anon");
        map.put("/css/**","anon");
        map.put("/img/**","anon");
        map.put("/fonts/**","anon");
        map.put("/favicon.ico","anon");
```
