---
layout: post
title:  "MySQL忘记root密码"
permalink: mysql-force-reset-root
tags: [开发环境,MySQL]
---

在my.cnf中设置加skip-grant-tables，重启，此时登录则不需要密码，设置密码，再去掉在my.cnf中设置加的skip-grant-tables

输入mysql后无需密码直接进入了mysql控制台

```
mysql> use mysql;
mysql> UPDATE user SET password=PASSWORD("root") WHERE user='root’;
mysql> FLUSH PRIVILEGES;
```
