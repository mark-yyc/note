#### mysql 配置步骤(默认端口3306)

+ apt-get update
+ apt-get install mysql-server
+ mysql_secure_installation
+ systemctl status mysql.service 查看服务状态
+ vi /etc/mysql/mysql.conf.d/mysqld.cnf
  + 注释bind-address=127.0.0.1
+ mysql -uroot -p 启动mysql
  + create user 'username'@'host' identified by 'password' 创建用户(host值访问者的ip地址，%代表全部)
  + grant all privileges on databasename.tablename to 'username'@'host' 授予权限 databasename和tablename可以用*代替，代表所有
  + flush privileges
  + Drop user 'username'@'host'