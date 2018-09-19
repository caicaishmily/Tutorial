## 什么是PostgreSQL？

- PostgreSQL是一个功能强大的开源对象关系数据库管理系统(ORDBMS)。 用于安全地存储数据; 支持最佳做法，并允许在处理请求时检索它们。

- PostgreSQL(也称为Post-gress-Q-L)由PostgreSQL全球开发集团(全球志愿者团队)开发。 它不受任何公司或其他私人实体控制。 它是开源的，其源代码是免费提供的。

- PostgreSQL是跨平台的，可以在许多操作系统上运行，如Linux，FreeBSD，OS X，Solaris和Microsoft Windows等。

## PostgreSQL历史

PostgreSQL由计算机科学教授Michael Stonebraker在UCB创建。 它最初叫做Postgres。 1986年由Michael Stonebraker教授作为后续项目和Ingres项目启动，克服了当代数据库系统的问题。 PostgreSQL现在是任何地方都很先进的开源数据库。

### 历史简介：

#### 1977 - 1985年：开发了一个名为INGRES的项目。

- 关系数据库的概念证明。
- 1980年成立Ingres公司。
- 1994年被Computer Associates购买。

#### 1986-1994: POSTGRES

- 开发INGRES中的概念，重点是面向对象和查询语言Quel。
- INGRES的代码基础未被用作POSTGRES的基础。
- 商业化为Illustra(由Informix购买，之后由IBM购买)。

#### 1994-1995: Postgres95

- 1994年增加了对SQL的支持。
- 1995年发布为Postgres95。
- 1996年重新发布为PostgreSQL 6.0。
- 建立PostgreSQL全球开发团队。

## PostgreSQL特点
- PostgreSQL可在所有主要操作系统(即Linux，UNIX(AIX，BSD，HP-UX，SGI IRIX，Mac OS X，Solaris，Tru64)和Windows等)上运行。
- PostgreSQL支持文本，图像，声音和视频，并包括用于C/C++，Java，Perl，Python，Ruby，Tcl和开放数据库连接(ODBC)的编程接口。
- PostgreSQL支持SQL的许多功能，例如复杂SQL查询，SQL子选择，外键，触发器，视图，事务，多进程并发控制(MVCC)，流式复制(9.0)，热备(9.0))。
- 在PostgreSQL中，表可以设置为从“父”表继承其特征。
- 可以安装多个扩展以向PostgreSQL添加附加功能。

### PostgreSQL工具
1. psql：
它是一个命令行工具，也是管理PostgreSQL的主要工具。 pgAdmin是PostgreSQL的免费开源图形用户界面管理工具。

2. phpPgAdmin:
它是用PHP编写的PostgreSQL的基于Web的管理工具。 它基于phpMyAdmin工具管理MySQL功能来开发。它可以用作PostgreSQL的前端工具。

3. pgFouine：
它是一个日志分析器，可以从PostgreSQL日志文件创建报告。 专有工具有 -
Lightning Admin for PostgreSQL, Borland Kylix, DBOne, DBTools Manager PgManager, Rekall, Data Architect, SyBase Power Designer, Microsoft Access, eRWin, DeZign for Databases, PGExplorer, Case Studio 2, pgEdit, RazorSQL, MicroOLAP Database Designer, Aqua Data Studio, Tuples, EMS Database Management Tools for PostgreSQL, Navicat, SQL Maestro Group products for PostgreSQL, Datanamic DataDiff for PostgreSQL, Datanamic SchemaDiff for PostgreSQL, DB MultiRun PostgreSQL Edition, SQLPro, SQL Image Viewer, SQL Data Sets 等等。

## PostgreSQL数据类型
数据类型指定要在表字段中存储哪种类型的数据。 在创建表时，对于每列必须使用数据类型。
PotgreSQL中主要有三种类型的数据类型。 此外，用户还可以使用CREATE TYPE SQL命令创建自己的自定义数据类型。

以下是PostgreSQL中主要有三种类型的数据类型：

- 数值数据类型
- 字符串数据类型
- 日期/时间数据类型

## PostgreSQL 常用命令
- 导入sql:  
 psql -d 数据库名 -h ip地址 -p 数据库端口 -U 用户名 -f 文件地址
