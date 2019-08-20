### 参考
https://www.aliyun.com/jiaocheng/126382.html

### 下载
[phpadmin](https://www.phpmyadmin.net/downloads/)

### 环境配置
```
(1)安装LAMP

[ aliyunzixun@xxx.com ~]# yum install httpd php mariadb-server –y
(2)安装php链接数据库的扩展程序包

[ aliyunzixun@xxx.com ~]# yum install php-mysql
(3)安装支持多字节字符串扩展的程序包

[ aliyunzixun@xxx.com ~]# yum install php-mbstring -y
(4)安装支持多加密扩展的程序包

[ aliyunzixun@xxx.com ~]# yum install php-mcrypt –y 2 phpmyadmin配置
```

防火墙运行访问80端口
```
输入 /sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT
```

### centos7安装php5
参考:
http://www.blogjava.net/nkjava/archive/2015/01/20/422289.html