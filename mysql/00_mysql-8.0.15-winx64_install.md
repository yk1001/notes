1,���� mysql-8.0.15-winx64
---
	https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.15-winx64.zip
2����ѹ�����û�������
---
	MYSQL_HOME=D:\dev\mysql-8.0.15-winx64
	path=%MYSQL_HOME%\bin;...
3,�½���MYSQL_HOME���½�my.ini�ļ���ע���޸�basedir��datadir
---
	#my.ini ��������
	[mysql]
	#����mysql�ͻ���Ĭ���ַ���
	default-character-set=utf8
	[mysqld]
	#����3306�˿�
	port = 3306 
	#����mysql�İ�װĿ¼
	basedir=D:\dev\mysql-8.0.15-winx64
	#����mysql���ݿ�����ݵĴ��Ŀ¼
	datadir=D:\dev\mysql-8.0.15-winx64\data
	#�������������
	max_connections=200
	#�����ʹ�õ��ַ���Ĭ��Ϊ8���ر����latin1�ַ���
	character-set-server=utf8
	#�����±�ʱ��ʹ�õ�Ĭ�ϴ洢����
	default-storage-engine=INNODB
4,Ctrl + R,����cmd,�������������
---
	mysqld --install
	#�س�����ʾ��Service successfully installed��˵��ע�����ɹ�
5����ȡ��ʼ���룬��ѡһ���Ƽ��ڶ��֣�
---
	1������mysqld  --initialize�����ʼ��mysql��data����Ŀ¼����ʼ����Ϻ󣬻��ڽ�ѹĿ¼������һ��data�ļ��У� ������ļ�������һ��.err��β���ļ����򿪺����������ɵ����롣
	2��ʹ��mysqld --initialize --console��������������
6����������net start mysql
---
7��ʹ����������¼���޸����� 
---
	mysql -u root -p #����������ɵ�����
	ALTER USER USER() IDENTIFIED BY '������';
	