1,拉取mysql8的镜像
---
	docker pull registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
2,master mysql 配置
---
	mkdir -p /var/mysql1/conf
	mkdir -p /var/mysql1/data
	vi /var/mysql1/conf/config-file.cnf
	[mysqld]
	#允许最大连接数
	max_connections=200
	#服务端使用的字符集默认为8比特编码的latin1字符集
	character-set-server=utf8
	#创建新表时将使用的默认存储引擎
	default-storage-engine=INNODB
	#default-authentication-plugin=mysql_native_password
	sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
	log-bin=/var/lib/mysql/binlog
	server-id=3306
	binlog-do-db=test
3,slave mysql 配置
---
	mkdir -p /var/mysql2/conf
	mkdir -p /var/mysql2/data
	vi /var/mysql2/conf/config-file.cnf
	[mysqld]
	#允许最大连接数
	max_connections=200
	#服务端使用的字符集默认为8比特编码的latin1字符集
	character-set-server=utf8
	#创建新表时将使用的默认存储引擎
	default-storage-engine=INNODB
	#default-authentication-plugin=mysql_native_password
	sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
	server-id=3406
	log-bin=/var/lib/mysql/binlog
4,启动master
---
	sudo docker run --name mysql1 -v /var/mysql1/conf:/etc/mysql/conf.d -v /var/mysql1/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
	docker exec -it ${cid} bash
	mysql -u root -p
	输入密码 123456
	#修改root密码的加密方式，使得navicat可以访问
	grant all PRIVILEGES on *.* to root@'%' WITH GRANT OPTION;
	ALTER user 'root'@'%' IDENTIFIED WITH mysql_native_password BY'123456';
	FLUSH PRIVILEGES;
5,启动slave
---
	sudo docker run --name mysql2 -v /var/mysql2/conf:/etc/mysql/conf.d -v /var/mysql2/data:/var/lib/mysql -p 3406:3306 -e MYSQL_ROOT_PASSWORD=123456 -d registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
	仿照步骤4,修改root的密码
6,主从配置
---
	进入master，这时master不允许更新，
	show master status
	并记录：file position
	#1.先对主库锁表 FLUSH TABLES WITH READ LOCK;
	#2.备份数据 mysqldump -uroot -p -hlocalhost > mysql.bak.sql
	#3.解锁主库 unlock tables;
	
	进入slave,
	change master to master_host='172.17.0.2',master_port=3306,master_user='root',master_password='123456',master_log_file='binlog.000004',master_log_pos=2774;
	#master_host 到master容器中查看 cat /etc/hosts
	#master_log_file 为master上'show master status' 时记录的file
	#master_log_pos 为master上'show master status' 时记录的position
	start slave
6，验证
---
       进入slave,
	show slave status 
	#slave_io_state 变为 Waiting for master to send event
	#slave_io_running 和 slave_sql_running 都为yes
	
	进入master,执行下面的sql
	create database test default charset utf8;
	CREATE TABLE test.t1
	(
		id int,
		last_name varchar(255),
		first_name varchar(255)
	);
	insert into test.t1(id,last_name,first_name) values (1,'last1','first1');
	
	再进入 slave,查看是否test库已创建，并且t1中有记录
7，主从是否同步检测
---
	进入 master 执行
	show master status
	进入slave 执行
	show slave status 
	比较 position 和 read_master_log_pos
	