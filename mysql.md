#mysql
##常用命令
###安装

sudo apt-get install mysql-server mysql-client #中途会让你输入一次root用户密码

###进入mysql

mysql -u root -p

#修改 MySQL 的管理员密码

sudo mysqladmin -u root password newpassword；

##无法登录错误
###第一种办法
steve@steve:~$ mysql --user=root --pass mysql
Enter password:

mysql> update user set Password=PASSWORD('new-password-here') WHERE User='root';
Query OK, 2 rows affected (0.04 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> flush privileges;
Query OK, 0 rows affected (0.02 sec)

mysql> exit
Bye

###重设密码

sudo /etc/init.d/mysql stop

sudo /usr/bin/mysqld_safe --skip-grant-tables &

sudo mysql --user=root mysql

mysql> update user set Password=PASSWORD('new-password-here') WHERE User='root';

mysql> flush privileges;

mysql> exit




