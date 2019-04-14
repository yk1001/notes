1,��ȡmysql8�ľ���
---
	docker pull registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
2,master mysql ����
---
	mkdir -p /var/mysql1/conf
	mkdir -p /var/mysql1/data
	vi /var/mysql1/conf/config-file.cnf
	[mysqld]
	#�������������
	max_connections=200
	#�����ʹ�õ��ַ���Ĭ��Ϊ8���ر����latin1�ַ���
	character-set-server=utf8
	#�����±�ʱ��ʹ�õ�Ĭ�ϴ洢����
	default-storage-engine=INNODB
	#default-authentication-plugin=mysql_native_password
	sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
	log-bin=/var/lib/mysql/binlog
	server-id=3306
	binlog-do-db=test
3,slave mysql ����
---
	mkdir -p /var/mysql2/conf
	mkdir -p /var/mysql2/data
	vi /var/mysql2/conf/config-file.cnf
	[mysqld]
	#�������������
	max_connections=200
	#�����ʹ�õ��ַ���Ĭ��Ϊ8���ر����latin1�ַ���
	character-set-server=utf8
	#�����±�ʱ��ʹ�õ�Ĭ�ϴ洢����
	default-storage-engine=INNODB
	#default-authentication-plugin=mysql_native_password
	sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
	server-id=3406
	log-bin=/var/lib/mysql/binlog
4,����master
---
	sudo docker run --name mysql1 -v /var/mysql1/conf:/etc/mysql/conf.d -v /var/mysql1/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
	docker exec -it ${cid} bash
	mysql -u root -p
	�������� 123456
	#�޸�root����ļ��ܷ�ʽ��ʹ��navicat���Է���
	grant all PRIVILEGES on *.* to root@'%' WITH GRANT OPTION;
	ALTER user 'root'@'%' IDENTIFIED WITH mysql_native_password BY'123456';
	FLUSH PRIVILEGES;
5,����slave
---
	sudo docker run --name mysql2 -v /var/mysql2/conf:/etc/mysql/conf.d -v /var/mysql2/data:/var/lib/mysql -p 3406:3306 -e MYSQL_ROOT_PASSWORD=123456 -d registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
	���ղ���4,�޸�root������
6,��������
---
	����master����ʱmaster��������£�
	show master status
	����¼��file position
	#1.�ȶ��������� FLUSH TABLES WITH READ LOCK;
	#2.�������� mysqldump -uroot -p -hlocalhost > mysql.bak.sql
	#3.�������� unlock tables;
	
	����slave,
	change master to master_host='172.17.0.2',master_port=3306,master_user='root',master_password='123456',master_log_file='binlog.000004',master_log_pos=2774;
	#master_host ��master�����в鿴 cat /etc/hosts
	#master_log_file Ϊmaster��'show master status' ʱ��¼��file
	#master_log_pos Ϊmaster��'show master status' ʱ��¼��position
	start slave
6����֤
---
       ����slave,
	show slave status 
	#slave_io_state ��Ϊ Waiting for master to send event
	#slave_io_running �� slave_sql_running ��Ϊyes
	
	����master,ִ�������sql
	create database test default charset utf8;
	CREATE TABLE test.t1
	(
		id int,
		last_name varchar(255),
		first_name varchar(255)
	);
	insert into test.t1(id,last_name,first_name) values (1,'last1','first1');
	
	�ٽ��� slave,�鿴�Ƿ�test���Ѵ���������t1���м�¼
7�������Ƿ�ͬ�����
---
	���� master ִ��
	show master status
	����slave ִ��
	show slave status 
	�Ƚ� position �� read_master_log_pos
	