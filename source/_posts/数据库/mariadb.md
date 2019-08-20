### 下载
1. mariadb下载地址[mariadb](https://downloads.mariadb.org/mariadb/)
2. mysqlworkbench下载地址
[mysqlworkbench](https://dev.mysql.com/downloads/workbench/)

### 安装mariadb
1.解压下载的软件
```bash
[ruby@batman source]$ tar xvf mariadb-10.3.10-linux-x86_64.tar.gz
[ruby@batman source]$ sudo mv mariadb-10.3.10-linux-x86_64 /usr/local/mysql
```
2.添加mariadb用户，属组
```
# groupadd mysql                     增加 mysql 属组 
# useradd -g mysql mysql     增加 mysql 用户 并归于mysql 属组 
# chown mysql:mysql -Rf  /usr/local/mysql     设置 mysql 目录的用户及用户组归属。 
# chmod +x -Rf /usr/local/mysql    赐予可执行权限 
# cp /usr/local/mysql/support-files/my-medium.cnf /etc/my.cnf     复制默认mysql配置 文件到/etc 目录 
# /usr/local/mysql/scripts/mysql_install_db --user=mysql   初始化数据 库 
# cp  /usr/local/mysql/support-files/mysql.server    /etc/init.d/mysql   复制mysql服务程序 到系统 目录 
# chkconfig  mysql on   添加mysql 至系统服务并设置为开机启动
```
3.修正权限
```
# service  mysql  start  启动mysql
#vim /etc/profile   编辑profile,将mysql的可执行路径加入系统PATH
export PATH=/usr/local/mysql/bin:$PATH 
#source /etc/profile  使PATH生效。
#mysqladmin -u root password 'yourrootpassword' 设定root账号及密码
#mysql -uroot -p  使用root用户登录mysql
[none]>use mysql  切换至mysql数据库。
[mysql]>select user,host,password from user; --查看系统权限
[mysql]>drop user ''@'localhost'; --删除不安全的账户
[mysql]>drop user root@'::1';
[mysql]>drop user root@127.0.0.1;
。。。
[mysql]>select user,host,password from user; --再次查看系统权限，确保不安全的账户均被删除。

[mysql]>flush privileges;  --刷新权限

1）修改字符集为UTF8
#vi /etc/my.cnf
在[client]下面添加 default-character-set = utf8
在[mysqld]下面添加 character_set_server = utf8
修改完重启：#service  mysql  restart 

2）增加错误日志
#vi /etc/my.cnf
在[mysqld]下面添加：
log-error = /usr/local/mysql/log/error.log
general-log-file = /usr/local/mysql/log/mysql.log
修改完重启：#service  mysql  restart 

3) 设置为不区分大小写，linux下默认会区分大小写。
#vi /etc/my.cnf
在[mysqld]下面添加：
lower_case_table_name=1
修改完重启：#service  mysql  restart  
```

4.连接上数据库
```
[ruby@batman ~]$ mysql -uroot -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 10
Server version: 10.3.10-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> \h

General information about MariaDB can be found at
http://mariadb.org

List of all MySQL commands:
Note that all text commands must be first on line and end with ';'
?         (\?) Synonym for `help'.
clear     (\c) Clear the current input statement.
connect   (\r) Reconnect to the server. Optional arguments are db and host.
delimiter (\d) Set statement delimiter.
edit      (\e) Edit command with $EDITOR.
ego       (\G) Send command to mysql server, display result vertically.
exit      (\q) Exit mysql. Same as quit.
go        (\g) Send command to mysql server.
help      (\h) Display this help.
nopager   (\n) Disable pager, print to stdout.
notee     (\t) Don't write into outfile.
pager     (\P) Set PAGER [to_pager]. Print the query results via PAGER.
print     (\p) Print current command.
prompt    (\R) Change your mysql prompt.
quit      (\q) Quit mysql.
rehash    (\#) Rebuild completion hash.
source    (\.) Execute an SQL script file. Takes a file name as an argument.
status    (\s) Get status information from the server.
system    (\!) Execute a system shell command.
tee       (\T) Set outfile [to_outfile]. Append everything into given outfile.
use       (\u) Use another database. Takes database name as argument.
charset   (\C) Switch to another charset. Might be needed for processing binlog with multi-byte charsets.
warnings  (\W) Show warnings after every statement.
nowarning (\w) Don't show warnings after every statement.

For server side help, type 'help contents'

MariaDB [(none)]>
```

5.远程连接
```
mysql -h <endpoint> -P 3306 -u <mymasteruser>
```

6.查看mysql使用的端口
```
[root@DOSFO2 volume-sfo2-01]# netstat -apn | grep mysql
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN      2472/mysqld
unix  2      [ ACC ]     STREAM     LISTENING     106927   2472/mysqld
```
如果没有要设置mysqld运行绑定的ip地址，在my.conf中加入
```
bind-address=0.0.0.0
```

7.查看mysql启动方式
```
[ruby@batman ~]$ ps aux|grep mysql
root      2156  0.0  0.3 115444  3308 ?        S    09:52   0:00 /bin/sh /usr/local/mysql/bin/mysqld_safe --datadir=/var/lib/mysql --pid-file=/var/lib/mysql/batman.pid
mysql     2247  0.3  8.6 1255448 87464 ?       Sl   09:52   0:00 /usr/local/mysql/bin/mysqld --basedir=/usr/local/mysql --datadir=/var/lib/mysql --plugin-dir=/usr/local/mysql/lib/plugin --user=mysql --log-error=/var/log/mariadb/mariadb.log --pid-file=/var/lib/mysql/batman.pid --socket=/tmp/mysq .sock
ruby      2304  0.0  0.2 112716  2316 pts/2    S+   09:53   0:00 grep --color=auto mysql
```
可以通过删除data目录/var/lib/mysql重新构建数据库

### 使用
1.自动补全
MyCli是MySQL，MariaDB和Percona的命令行界面，具有自动完成和语法高亮的功能。
通过pip安装
```
pip install mycli
```
通过mycli连接mysql数据库
```
mycli -u root -p xxx
```

使用MYSQL -I命令，查看MYSQL命令的参数，其中对--auto-rehash参数的说明如下：
--auto-rehash     Enable automatic rehashing. One doesn't need to use
                  'rehash' to get table and field completion, but startup
                  and reconnecting may take a longer time. Disable with
                  --disable-auto-rehash.
有两个方法：

修改my.cnf
vi /etc/my.cnf 
[mysql] 
auto-rehash         #添加auto-rehash
注：修改 #no-auto-rehash 去掉# 改为上面那一条
重启mysql服务
然后登陆mysql即可补全

客户端连接mysql时
在mysql启动时加参数auto-rehash 
mysql –uroot -pmysql --auto-rehash 