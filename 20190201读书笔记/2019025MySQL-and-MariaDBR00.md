## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 总体

除了本书，O'Reilly 还出版了其他一些值得入手的 MySQL 相关书籍。它主推的 MySQL 参考书是我写的《MySQL 核心技术手册》。如果需要解决现实中的常见问题，可参考 Paul DuBois 的《MySQL Cookbook（中文版）》。若是需要调优和性能监控方面的建议，如数据库备份，则可参考 Baron Schwartz、Peter Zaitsev 和 Vadim Tkachenko 合著的《高性能 MySQL》。

安装新版时显示的信息：

```
==> protobuf@3.7

protobuf@3.7 is keg-only, which means it was not symlinked into /usr/local, because this is an alternate version of another formula.

If you need to have protobuf@3.7 first in your PATH run:

    echo 'export PATH="/usr/local/opt/protobuf@3.7/bin:$PATH"' >> ~/.zshrc

For compilers to find protobuf@3.7 you may need to set:

export LDFLAGS="-L/usr/local/opt/protobuf@3.7/lib"

export CPPFLAGS="-I/usr/local/opt/protobuf@3.7/include"

For pkg-config to find protobuf@3.7 you may need to set:

xport PKG_CONFIG_PATH="/usr/local/opt/protobuf@3.7/lib/pkgconfig"

==> mysql

We've installed your MySQL database without a root password. To secure it run:

mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:

mysql -uroot

To have launchd start mysql now and restart at login:

brew services start mysql

Or, if you don't want/need a background service you can just run:

mysql.server start
```

账户安全相关的一系列设置可以通过命令 `mysql_secure_installation` 来完成。

## 0201. 安装

1、MySQL 与 MariaDB 涉及到的软件。

服务器 mysqld 和客户端 mysql。1）MySQL 和 MariaDB 的安装包带有几个程序。其中最主要的是服务器程序，即 mysqld 守护进程，它在 MySQL 和 MariaDB 中是同名的。这个守护进程是对整个数据库进行存储和操控的实际执行者。它监听着一个特定的端口（默认是 3306），这个端口供用户提交查询。2）标准的 MySQL 客户端就叫作 mysql，用户可使用它的命令行接口登录和执行 SQL 查询。该客户端还能接受含有查询命令的文本文件，代表用户或其他软件执行查询。不过，我们大多使用各种编程语言来跟 MySQL 交互。所谓守护进程，就是一个在后台持续运行的进程，这是 Unix 中的术语，而大多数人就叫它「服务器」。

2、Mac 上查看是否安装；

命令行内输入命令 

```
whereis mysql mysqld mysqld_safe
```

接着检查服务器 mysqld 有没有在运行，输入命令 

```
ps aux | grep mysql
```

如果没有运行的话，输入命令 /usr/bin/mysqld_safe & 以 root 身份启动它；

3、Mac 上安装；

```
update user set password=password('') where user='root';
```

Mac 上用 brew 安装 mysql，安装后在 `/usr/local/var/` 里面。

安装完成后 mysql 是没有启动的，命令行里输入命令 `mysql.server start `来启动；同理推测关闭服务器是 `mysql.server stop`。

修改原始密码；输入命令 mysqladmin -u root -p flush-privileges password 修改，原始的是空的直接 enter 会让你连续 2 次输入新密码的 (dalongsql)；设置完之后会跳出；

Warning: Since password will be sent to server in plain text, use ssl connection to ensure password safety.

设置 my.cnf

通过 brew 安装的 mysql 似乎默认并没有使用 my.cnf，直接使用默认配置启动 my.cnf 文件位置；

输入命令 mysql --help | grep 'Default options' -A 1 可以跳出下列说明；

Default options are read from the following files in the given order:

/etc/my.cnf /etc/mysql/my.cnf /usr/local/etc/my.cnf ~/.my.cnf

mysql 会按照以上情况顺序加载 mysql，建议直接在第一个路径下新建一个，即 /etc/my.cnf；

记住要用 root 身份新建这个文件；sudo vi /etc/my.cnf

my.cnf 文本内容如下；

[mysqld]

datadir=/data/mysql

user=mysql

default-character-set=utf8

log-bin=/data/mysql/logs/binary_log

max_allowed_packet=521M

ulimit -d 256000

ledir=/usr/sbin

mysqld=mysqld

log-error=/var/log/mysqld.log

pid-file=/data/mysql/mysqld.pid

[mysql.client]

default-character-set=utf8

## 0301. 基础知识和 mysql 客户端

1、登入 mysql；

先启动服务器；mysql.server start

root 用户登入命令；mysql -u root -p

选项 - u 是 user，所以后面接用户名；选项 - p 是 password，这个是用密码登录的意思，也可以直接在后面接密码接着登入 (mysql -u dalong -pdalong0514)，但这样密码可以显示在屏幕上，不安全。

注意登入 mysql 后，里面的命令都是以分号 ；结束的。

2、创建用户；

查看目前服务器上的用户情况，输入命令：

    mysql -u root -p -e "SELECT User,Host FROM mysql.user";

以 root 身份登入后，只需命令：

    SELECT User,Host FROM mysql.user;

创建普通用户，输入命令：

    mysql -u root -p -e "GRANT USAGE ON *.* TO ‘dalong'@'localhost' IDENTIFIED BY ‘dalong0514';"

上面的命令是建立名为 dalong 的用户，并允许它从 localhost 登录 MySQL。其中 *.* 表示所有数据库和所有表。更详细的解释会在后面讲到。同时这里将其密码设置为 dalong0514。

mac 上试验过，上面的方法不行，待解决。

使用 root 身份登入后，输入命令：

    CREATE USER ‘dalong’@‘localhost’ IDENTIFIED BY ‘dalong0514’;

『注意，必须增加手动输入命令，复制过来的不行，目前不知道何种原因。』

给用户赋予权限，输入命令；

    mysql -u root -p -e "GRANT ALL ON *.* TO ‘dalong'@'localhost'";

dalong@localhost 就有了所有的基本权限，建立这样一个功能齐全的用户，以便在学习本书的过程中随便试验。

想知道某个用户所拥有的权限，输入命令；

mysql -u root -p -e "SHOW GRANTS FOR 'russell'@'localhost' \G"

也可以输入命令：

    show grants for dalong@localhost; 

来查看用户所拥有的权限。

3、查看服务器上现有的数据库：

    show databases;

4、创建和删除数据库：

建一个名为 test 的数据库：

    create database test;

删除该数据库的话：

    drop database test;

5、在数据库里创建一个表，查看数据库里的表，在 test 数据库里创建 books 这个表：

    CREATE TABLE test.books (book_id INT, title TEXT, status INT); 

查看数据库 test 里的表 books：

    SHOW TABLES FROM test; 

6、切换到某个数据库里去

    USE test;

切换之后再产看该数据库里的表直接可以省略后面的 from test 了；直接 

    SHOW TABLES;

7、查看表格的具体结构参数；

    DESCRIBE books;

8、往数据库里添加数据的命令；

    INSERT INTO books VALUES(100, 'Heart of Darkness', 0); 

9、查看表里所有数据；

    select * from books;

附加条件的话：

    select * from books where status=1;

如果数据较多，可以用另外一个格式表现，语句后加 \G，注意必须是大写的 G，且没有分好结尾。

    select * from books where status=1 \G

10、更新数据库：

     update books set status=1 where book_id=100;

11、联立 2 个表的方式；

    SELECT book_id, title, status_name

    FROM books JOIN status_names

    WHERE status = status_id;

12、退出 mysql，输入命令：

exit;

13、mysql 的命令都是以分号 ；结尾的。

本书第二篇；数据结构；

## 0401. 创建数据库和表

1、创建表的时候可以加上一些选项；

详见 P46 的命令；

