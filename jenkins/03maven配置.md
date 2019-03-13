1,下载apache-maven-3.3.9-bin.tar.gz
---
2，上传到jenkins服务器，解压
---
	tar -zxf apache-maven-3.3.9-bin.tar.gz
3,移动解压后的文件夹，到/var/jenkins_home
---
	mv apache-maven-3.3.9 /var/jenkins_home
4,设置全局工具配置
---
	MAVN_HOME-/var/jenkins_home/apache-maven-3.3.9
	#注意 maven settings.xml文件配置合适的镜像地址，方便拉取jar包
  	Default settings provider	  = /var/jenkins_home/apache-maven-3.3.9/conf/settings.xml
  	Default global settings provider	 = /var/jenkins_home/apache-maven-3.3.9/conf/settings.xml