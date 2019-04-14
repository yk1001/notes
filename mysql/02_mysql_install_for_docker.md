1,下载官方docker
---
	docker pull mysql:8.0
	#docker pull registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
2,创建挂载目录
---
	mkdir -p /var/mysql/conf
	mkdir -p /var/mysql/data
3,在目录/var/mysql/conf 创建文件 config-file.cnf
---
	[mysqld]
	#允许最大连接数
	max_connections=200
	#服务端使用的字符集默认为8比特编码的latin1字符集
	character-set-server=utf8
	#创建新表时将使用的默认存储引擎
	default-storage-engine=INNODB
	default-authentication-plugin=mysql_native_password
	sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
4,启动docker images
---
	sudo docker run --name mysql -v /var/mysql/conf:/etc/mysql/conf.d -v /var/mysql/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
	#/etc/mysql/conf.d 是镜像中默认自定义配置文件的地址，该文件中配置会覆盖 my.cnf默认配置
	#/var/lib/mysql 是镜像中默认datadir目录
5,验证
---
	navicat 或其他客户端 进行连接验证
	ls -a /var/mysql/data #进行目录挂载验证
	
