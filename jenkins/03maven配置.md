1,����apache-maven-3.3.9-bin.tar.gz
---
2���ϴ���jenkins����������ѹ
---
	tar -zxf apache-maven-3.3.9-bin.tar.gz
3,�ƶ���ѹ����ļ��У���/var/jenkins_home
---
	mv apache-maven-3.3.9 /var/jenkins_home
4,����ȫ�ֹ�������
---
	MAVN_HOME-/var/jenkins_home/apache-maven-3.3.9
	#ע�� maven settings.xml�ļ����ú��ʵľ����ַ��������ȡjar��
  	Default settings provider	  = /var/jenkins_home/apache-maven-3.3.9/conf/settings.xml
  	Default global settings provider	 = /var/jenkins_home/apache-maven-3.3.9/conf/settings.xml