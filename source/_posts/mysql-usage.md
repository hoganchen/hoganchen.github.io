---
title: mysql使用问题记录
date: 2018-06-11 16:12:49
tags:
---

<!-- more -->

<ol>

##### <li> Window安装mysql 5.7.19压缩包
https://my.oschina.net/u/2557245/blog/876028
http://www.jianshu.com/p/b601097ef5c9
http://www.phperz.com/article/16/0703/231878.html
http://blog.csdn.net/tanghong1996/article/details/71330666
http://www.bkjia.com/Mysql/1198992.html
http://www.bkjia.com/Mysql/1221297.html
http://www.cnblogs.com/ldybyz/p/7138444.html
http://www.2cto.com/database/201707/660725.html

```
1. 解压缩压缩包

2. 设置环境变量
新建MYSQL_HOME变量值为刚才下载解压缩后的自定义目录的bin目录下
如：
MYSQL_HOME: D:\Codes\mysql-5.7.19-winx64
PATH环境变量添加Mysql的路径: %MYSQL_HOME%\bin

3. 以管理员身份运行命令提示符
cd D:\Codes\mysql-5.7.19-winx64\bin

4. 安装myql
mysqld install

5. 初始化data目录
https://dev.mysql.com/doc/refman/5.7/en/data-directory-initialization-mysqld.html

mysqld --initialize --console
mysqld --initialize-insecure --console

从5.7.6版开始，Zip压缩包不再提供data目录，所以也不会有MySQL系统数据库的数据文件，我们需要使用mysqld --initialize或者--initialize-insecure对数据库进行初始化

--initialize：初始化时会随机生成一个root用户密码，改密码会以日志的方式打印出来，如果控制台没有密码可能记录在日志文件下，在Windows上可以使用--console选项把信息打印到控制台。使用mysqld –initialize方法安装会生成一个随机字符串组成的密码，这个密码在错误日志<mysql解压目录>\data\<计算机用户名>.err中可以找到。

--initialize-insecure：不会生成随机密码，但是在登录服务器是可以使用--skip-password跳过密码输入：mysql -u root --skip-password。

6. 启动mysql服务
net start mysql
```

##### <li> Window卸载mysql
```
以下命令都在cmd中执行，cmd需要以管理员身份运行，即找到cmd程序的路径，然后右键单击选择以管理员身份运行即可，cmd程序的路径为：C:\Windows\System32

1. 停止服务
net stop mysql

2. 删除服务
mysqld --remove mysql
sc delete mysql

3. 删除文件夹

4. 删除注册表
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Eventlog\Application\MySQL 目录删除
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\Eventlog\Application\MySQL 目录删除
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application\MySQL 目录删除

注册表中的ControlSet001、ControlSet002不一定是001和002，可能是ControlSet005、006之类，删除的时候都删除就可以 。
```

##### <li> 数据库备份与恢复
http://www.cnblogs.com/zhoujinyi/p/5684903.html

```
1. 备份
hogan@ubuntu:/tmp$ mysqlpump -uroot -p'rO0t@stck5ql*' -h127.0.0.1 --single-transaction --default-character-set=utf8 --default-parallelism=5 -B stock | gzip > ./stck_db_hp.sql.gz

2. 恢复
hogan@ubuntu:/tmp$ gzip -d stck_db.sql.gz
hogan@ubuntu:/tmp$ mysql -u root -p'rO0t@stck5ql*' < /tmp/stck_db.sql
```

##### <li> Mysql忘记密码
https://www.skyf.org/reset-mysql579-root-password/
https://my.oschina.net/shf/blog/545684
http://blog.csdn.net/stubbornness1219/article/details/53445904
http://blog.csdn.net/u013378306/article/details/50466073

```
http://www.cnblogs.com/yuxc/archive/2012/07/25/2607587.html
可能不适用于5.7

1、结束当前正在运行的mysql进程。
# /etc/init.d/mysql stop

2、用mysql安全模式运行并跳过权限验证。
# /usr/bin/mysqld_safe --skip-grant-tables

3、重开一个终端以root身份登录mysql。
# mysql -u root

4、修改root用户口令。
mysql> use mysql;
Reading table information for completion of table and column namesYou can turn off this feature to get a quicker startup with -A
Database changed

mysql> update user set Password = PASSWORD('root') where User ='root';
Query OK, 3 rows affected (0.00 sec)
Rows matched: 3  Changed: 3  Warnings: 0

mysql> exit

5、结束mysql安全模式，用正常模式运行mysql。
# /etc/init.d/mysql restart

6、试试你新修改的口令
mysql> show grants for 'root'@'127.0.0.1';
mysql> flush privileges；
mysql> quit
```

##### <li> Mysql虚拟表
http://yypiao.iteye.com/blog/2359859
http://www.cnblogs.com/jevo/p/3262227.html
http://www.nowamagic.net/librarys/veda/detail/1405
http://2853725.blog.51cto.com/2843725/1394430

##### <li> 临时表
http://blog.sae.sina.com.cn/archives/4096
http://www.runoob.com/mysql/mysql-temporary-tables.html

##### <li> Mysql慢查询
http://www.jianshu.com/p/7529a0fbf088
https://tech.meituan.com/mysql-index.html
https://www.kancloud.cn/thinkphp/mysql-design-optimalize/39320
https://flyerboy.github.io/2016/12/23/mysql_slow/
http://www.cnblogs.com/ggjucheng/archive/2012/11/11/2765237.html

##### <li> Mysql排序
http://www.runoob.com/mysql/mysql-order-by.html
```
语法

以下是 SQL SELECT 语句使用 ORDER BY 子句将查询数据排序后再返回数据：

SELECT field1, field2,...fieldN table_name1, table_name2...
ORDER BY field1, [field2...] [ASC [DESC]]

    你可以使用任何字段来作为排序的条件，从而返回排序后的查询结果。
    你可以设定多个字段来排序。
    你可以使用 ASC 或 DESC 关键字来设置查询结果是按升序或降序排列。 默认情况下，它是按升序排列。
    你可以添加 WHERE...LIKE 子句来设置条件。

select * from basics_data where pe > 0 and pb > 0 order by pb limit 10;

两个字段升序，默认情况下，它是按升序排列
select * from basics_data where pe > 0 and pb > 0 order by pb, pe limit 10;

一个字段升序，一个字段降序
select * from basics_data where pe > 0 and pb > 0 order by pb, pe desc limit 10;

```

##### <li> Mysql更新字段
http://www.runoob.com/mysql/mysql-alter.html
```
更改字段属性not null为null

alter table basics_data modify area varchar(4);
alter table area_data modify area varchar(6);


修改字段属性为not null
alter table basics_data modify area varchar(4) not null default "";
alter table area_data modify area varchar(6) not null default "";

修改默认值
mysql> alter table hist_day_data alter turnover set default 0;
mysql> alter table hist_week_data alter turnover set default 0;
mysql> alter table hist_month_data alter turnover set default 0;
```

##### <li> 删除数据
http://www.runoob.com/mysql/mysql-delete-query.html
```
mysql> delete from k_week_data where date = '2017-09-21';
Query OK, 2938 rows affected (1.87 sec)

mysql> select * from k_week_data where date = '2017-09-21';
Empty set (10.51 sec)

```

##### <li> Mysql索引
http://wiki.jikexueyuan.com/project/mysql/indexes.html
http://www.runoob.com/mysql/mysql-index.html
https://read01.com/78Ojo4.html
http://www.cnblogs.com/hustcat/archive/2009/10/28/1591648.html
https://segmentfault.com/a/1190000003072424
https://tech.meituan.com/mysql-index.html

```
数据库查询是数据库的最主要功能之一。我们都希望查询数据的速度能尽可能的快，因此数据库系统的设计者会从查询算法的角度进行优化。最基本的查询算法当然是顺序查找（linear search），这种复杂度为O(n)的算法在数据量很大时显然是糟糕的，好在计算机科学的发展提供了很多更优秀的查找算法，例如二分查找（binary search）、二叉树查找（binary tree search）等。如果稍微分析一下会发现，每种查找算法都只能应用于特定的数据结构之上，例如二分查找要求被检索数据有序，而二叉树查找只能应用于二叉查找树上，但是数据本身的组织结构不可能完全满足各种数据结构（例如，理论上不可能同时将两列都按顺序进行组织），所以，在数据之外，数据库系统还维护着满足特定查找算法的数据结构，这些数据结构以某种方式引用（指向）数据，这样就可以在这些数据结构上实现高级查找算法。这种数据结构，就是索引。

索引是在MYSQL的存储引擎层中实现的，而不是在服务层实现的。所以每种存储引擎的索引都不一定完全相同，也不是所有的存储引擎都支持所有的索引类型。MYSQL目前提供了一下4种索引。

    B-Tree 索引：最常见的索引类型，大部分引擎都支持B树索引。
    HASH 索引：只有Memory引擎支持，使用场景简单。
    R-Tree 索引(空间索引)：空间索引是MyISAM的一种特殊索引类型，主要用于地理空间数据类型。
    Full-text (全文索引)：全文索引也是MyISAM的一种特殊索引类型，主要用于全文索引，InnoDB从MYSQL5.6版本提供对全文索引的支持。

B-TREE索引类型
普通索引
    这是最基本的索引类型，而且它没有唯一性之类的限制。普通索引可以通过以下几种方式创建：
    （1）创建索引: CREATE INDEX 索引名 ON 表名(列名1，列名2,...);
    （2）修改表: ALTER TABLE 表名ADD INDEX 索引名 (列名1，列名2,...);
    （3）创建表时指定索引：CREATE TABLE 表名 ( [...], INDEX 索引名 (列名1，列名 2,...) );

UNIQUE索引
    表示唯一的，不允许重复的索引，如果该字段信息保证不会重复例如身份证号用作索引时，可设置为unique：
    （1）创建索引：CREATE UNIQUE INDEX 索引名 ON 表名(列的列表);
    （2）修改表：ALTER TABLE 表名ADD UNIQUE 索引名 (列的列表);
    （3）创建表时指定索引：CREATE TABLE 表名( [...], UNIQUE 索引名 (列的列表) );

主键：PRIMARY KEY索引
    主键是一种唯一性索引，但它必须指定为“PRIMARY KEY”。
    （1）主键一般在创建表的时候指定：“CREATE TABLE 表名( [...], PRIMARY KEY (列的列表) ); ”。
    （2）但是，我们也可以通过修改表的方式加入主键：“ALTER TABLE 表名ADD PRIMARY KEY (列的列表); ”。
    每个表只能有一个主键。 （主键相当于聚合索引，是查找最快的索引）
    注：不能用CREATE INDEX语句创建PRIMARY KEY索引

为表添加索引，可以采用4种语句。
    ALTER TABLE tbl_name ADD PRIMARY KEY (column_list) 该语句添加一个主键。意味着索引值必须是唯一的，不能为 NULL。
    ALTER TABLE tbl_name ADD UNIQUE index_name (column_list) 该语句为必须唯一的值（除了 NULL 值之外，NULL 值可以多次出现）创建索引。
    ALTER TABLE tbl_name ADD INDEX index_name (column_list) 语句为可能多次出现的值创建一般索引。
    ALTER TABLE tbl_name ADD FULLTEXT index_name (column_list) 语句创建专用于文本搜索的 FULLTEXT 索引。

```

##### <li> MySQL函数
```
查询结果求平均值

mysql> select avg(open), avg(close), avg(high), avg(low), max(high), min(low) from hist_day_data where code = '600000' and date >= '2017-10-09';

mysql> select avg(open) as openavg, avg(close), avg(high), avg(low), max(high), min(low) from hist_day_data where code = '600000' and date >= '2017-10-09';


```

##### <li> 查看警告信息
```
mysql> show warnings;
```