1,下载 mysql-8.0.15-winx64
---
	https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.15-winx64.zip
2，解压并设置环境变量
---
	MYSQL_HOME=D:\dev\mysql-8.0.15-winx64
	path=%MYSQL_HOME%\bin;...
3,新建在MYSQL_HOME下新建my.ini文件，注意修改basedir和datadir
---
	#my.ini 内容如下
	[mysql]
	#设置mysql客户端默认字符集
	default-character-set=utf8
	[mysqld]
	#设置3306端口
	port = 3306 
	#设置mysql的安装目录
	basedir=D:\dev\mysql-8.0.15-winx64
	#设置mysql数据库的数据的存放目录
	datadir=D:\dev\mysql-8.0.15-winx64\data
	#允许最大连接数
	max_connections=200
	#服务端使用的字符集默认为8比特编码的latin1字符集
	character-set-server=utf8
	#创建新表时将使用的默认存储引擎
	default-storage-engine=INNODB
4,Ctrl + R,输入cmd,打开命令行输入框
---
	mysqld --install
	#回车，提示：Service successfully installed，说明注册服务成功
5，获取初始密码，二选一（推荐第二种）
---
	1，输入mysqld  --initialize命令初始化mysql的data数据目录，初始化完毕后，会在解压目录下生成一个data文件夹， 在这个文件夹下有一个.err结尾的文件，打开后会有随机生成的密码。
	2，使用mysqld --initialize --console命令，生成随机密码
6，启动服务：net start mysql
---
7，使用随机密码登录并修改密码 
---
	mysql -u root -p #输入随机生成的密码
	ALTER USER USER() IDENTIFIED BY '新密码';
	