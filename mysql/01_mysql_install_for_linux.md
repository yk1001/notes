1��mysql8 ����
---
	https://dev.mysql.com/downloads/mysql/8.0.html
	ѡ�� Linux-Generic 32bit��64bit
	ѡ�� tar archive download
2����linux �Ͻ�ѹ tar��
---
	tar.xz ��ѹ���� tar -xvJf *.tar.xz
	mv ��ѹ���Ŀ¼�� /usr/local/mysql
3������/etc/my.cnf����socket�ļ���ַ
---
	groupadd mysql
	useradd -g mysql mysql
	#ע�⣬����/var/mysqlĿ¼,����Ŀ¼Ȩ����owner
4�����û���������ʹ��mysqld������path���ҵ�
---
5��mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
---
6��support-files/mysql.server start
---
7����log�в鿴 ��ʱroot���룬�鿴�Ƿ��б���
---
8����¼���������룬�����÷���
---
	mysql -uroot -p
	#ע��mysql8֮������ǿ��Ҫ���ߣ���ǿ�����룬���ñ���
10.����mysqldΪ���񣬿������Զ�����
---
	���ɾ������
	��ӣ� sudo update-rc.d ������ defaults
	ɾ����sudo update-rc.d -f ������ remove
	�������رա���������
	service ������ start
	service ������ stop
	service ������ start