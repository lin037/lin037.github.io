---
title: 启动mysql Job for mysqld.service failed because the control process exited with error code.
author: 林叁柒
date: 2020-05-04 14:53:17 +0800
categories: [数据库, MySQL]
tags: [数据库, MySQL, 报错, linux]
---

## 前言：
最近因为某多的一个活动，弄了200块钱，就开了台服务器耍耍；
服务器系统：centOS7；
然后我安装完mysql8.0.19后，启动时却报错了。
## 错误信息：

`Job for mysqld.service failed because the control process exited with error code. See "systemctl status mysqld.service" and "journalctl -xe" for details.`

使用命令查看日志信息

```powershell
cat /var/log/mysqld.log
```

日志显示为：

```powershell
2020-05-04T05:15:13.955353Z 0 [System] [MY-013169] [Server] /usr/sbin/mysqld (mysqld 8.0.19) initializing of server in progress as process 24414
2020-05-04T05:15:14.018517Z 0 [ERROR] [MY-010457] [Server] --initialize specified but the data directory has files in it. Aborting.
2020-05-04T05:15:14.018584Z 0 [ERROR] [MY-013236] [Server] The designated data directory /var/lib/mysql/ is unusable. You can remove all files that the server added to it.
2020-05-04T05:15:14.018686Z 0 [ERROR] [MY-010119] [Server] Aborting
2020-05-04T05:15:14.018903Z 0 [System] [MY-010910] [Server] /usr/sbin/mysqld: Shutdown complete (mysqld 8.0.19)  MySQL Community Server - GPL.
2020-05-04T05:15:42.115352Z 0 [System] [MY-013169] [Server] /usr/sbin/mysqld (mysqld 8.0.19) initializing of server in progress as process 24455
2020-05-04T05:15:42.118269Z 0 [ERROR] [MY-010457] [Server] --initialize specified but the data directory has files in it. Aborting.
2020-05-04T05:15:42.118312Z 0 [ERROR] [MY-013236] [Server] The designated data directory /var/lib/mysql/ is unusable. You can remove all files that the server added to it.
2020-05-04T05:15:42.118377Z 0 [ERROR] [MY-010119] [Server] Aborting
2020-05-04T05:15:42.118582Z 0 [System] [MY-010910] [Server] /usr/sbin/mysqld: Shutdown complete (mysqld 8.0.19)  MySQL Community Server - GPL.
2020-05-04T05:15:43.219050Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.0.19) starting as process 24457
2020-05-04T05:15:43.279094Z 1 [ERROR] [MY-011011] [Server] Failed to find valid data directory.
2020-05-04T05:15:43.279373Z 0 [ERROR] [MY-010020] [Server] Data Dictionary initialization failed.
2020-05-04T05:15:43.279871Z 0 [ERROR] [MY-010119] [Server] Aborting
2020-05-04T05:15:43.281231Z 0 [System] [MY-010910] [Server] /usr/sbin/mysqld: Shutdown complete (mysqld 8.0.19)  MySQL Community Server - GPL.

```

错误信息的摘要：

`initialize specified but the data directory has files in it. Aborting.`

`The designated data directory /var/lib/mysql/ is unusable. You can remove all files that the server added to it.`

`Failed to find valid data directory.`

`Data Dictionary initialization failed.`

`Aborting`

## 解决方法：
注意看日志的第三行：

`The designated data directory /var/lib/mysql/ is unusable. You can remove all files that the server added to it.`

翻译为：

`指定的数据目录/var/lib/mysql/不可用。您可以删除服务器添加到其中的所有文件。`

也就是说，只需要删除/var/lib/mysql文件即可。

在/var/lib目录下使用删除命令：

```powershell
rm -rf ./mysql
```
重新输入mysql初始化命令：

```powershell
mysqld --initialize
```
## 结果：

```powershell
[root@Lin037 lib]# systemctl start mysqld
[root@Lin037 lib]# systemctl status mysqld
● mysqld.service - MySQL Server
   Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2020-05-04 13:34:15 CST; 17s ago
     Docs: man:mysqld(8)
           http://dev.mysql.com/doc/refman/en/using-systemd.html
  Process: 24628 ExecStartPre=/usr/bin/mysqld_pre_systemd (code=exited, status=0/SUCCESS)
 Main PID: 24710 (mysqld)
   Status: "Server is operational"
   CGroup: /system.slice/mysqld.service
           └─24710 /usr/sbin/mysqld

May 04 13:33:53 cvm-3hcxgku26i225.novalocal systemd[1]: Starting MySQL Server...
May 04 13:34:15 cvm-3hcxgku26i225.novalocal systemd[1]: Started MySQL Server.
```

