1,下载jdk-8u131-linux-x64.tar.gz
---
2，上传到jenkins服务器，解压
---
	tar -zxf jdk-8u131-linux-x64.tar.gz
3,移动解压后的文件夹，到/var/jenkins_home
---
	mv jdk1.8.0_131 /var/jenkins_home
4,设置全局工具配置
---
	JAVA_HOME-/var/jenkins_home/jdk1.8.0_131