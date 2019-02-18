1，mysql8 下载
---
	https://dev.mysql.com/downloads/mysql/8.0.html
	选择 Linux-Generic 32bit或64bit
	选择 tar archive download
2，在linux 上解压 tar包
---
	tar.xz 解压命令 tar -xvJf *.tar.xz
	mv 解压后的目录到 /usr/local/mysql
3，创建/etc/my.cnf配置socket文件地址
---
	groupadd mysql
	useradd -g mysql mysql
	#注意，创建/var/mysql目录,配置目录权限与owner
4，配置环境变量，使得mysqld可以在path下找到
---
5，mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
---
6，support-files/mysql.server start
---
7，在log中查看 临时root密码，查看是否有报错
---
8，登录并重置密码，并设置访问
---
	mysql -uroot -p
	#注意mysql8之后密码强度要求变高，低强度密码，设置报错
10.设置mysqld为服务，开启就自动启动
---
	添加删除服务
	添加： sudo update-rc.d 服务名 defaults
	删除：sudo update-rc.d -f 服务名 remove
	启动、关闭、重启服务
	service 服务名 start
	service 服务名 stop
	service 服务名 start