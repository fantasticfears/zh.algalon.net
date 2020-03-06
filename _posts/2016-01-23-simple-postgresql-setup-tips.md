---
title: 极简 PostgreSQL 安装 Tips
tags:
  - PostgreSQL
---

[PostgreSQL](postgresql.org) 是一个 Client/Server 架构的数据库。Windows 安装器装的是服务器部分和命令行界面。服务器是在后台运行的，它没有界面，它显然也不需要界面，它的“界面”应该是 [SQL](https://zh.wikipedia.org/wiki/SQL)。

[pgAdmin III](http://www.pgadmin.org/index.php) 是图形化的管理工具。相对的就是命令行界面，这就是和 PostgreSQL 附带安装的 `pgsql`，也就是工具里的 shell。[phpPgAdmin](http://phppgadmin.sourceforge.net/) 是另一个 Web 版的 PHP 写的图形化的管理工具。

## Tips

PostgreSQL 作为一个数据库管理系统（Database Management System，DBMS），有访问控制等鉴权的功能。首先它是服务器，连接到服务器需要地址。装在本机，它的地址就是本机，即 localhost。Windows 的安装包，给 PostgreSQL 默认创建了 `postgres` 这个用户，密码在安装的时候已经为他设置了。有了这些信息，就可以操作 PostgreSQL 了，包括创建和导入新的数据库云云。

PostgreSQL 的鉴权是通过一个 `pg_hba.conf` 定义的，用户名和密码是其中一种验证身份的方法。PostgreSQL 能针对不用的数据库、不同的用户、不同的地址、不同的方法定义验证规则。绝大多数时候，为了省事，开发的时候可以把从 localhost 链接的所有数据库全部开放，这样就不用密码验证了。

PostgreSQL 用了标准的 POSIX 和 ISO C 的 locale 机制，就是 `LC_*`。在导入的时候出的错误，很有可能是因为 locale 的不符合，导致字符流中因为编码错误而判断出现了非法字符。换换 UTF-8 和 en_US 是不错的尝试思路。

`.sql` 是数据库的 dump 文件，导出了 PostgreSQL 的 schema 和真实数据，有了这个文件，就能够重新建立数据库。但是导入这个数据库文件前，你需要一个空的数据库。没有房间不能装家具。

## Hardcore Tips

PostgreSQL 创建数据库 `CREATE DATABASE` 的时候是[从模板创建](http://www.postgresql.org/docs/9.5/static/manage-ag-templatedbs.html)。他们叫 `template0` 和 `template1`。

PostgreSQL 的触发器、函数和语言支持应该是 DMBS 里最好的。这里概念多，有的和数据库理论相关，有的和实现相关。
