1, �����û�
---
	useradd jenkins
	usermod -g docker jenkins
2,��������Ŀ¼
---
	mkdir /var/jenkins_home
	chown -R 1000:1000 /var/jenkins_home
	chmod -R 777 /var/jenkins_home
3,���ؾ���
---
	docker pull registry.cn-hangzhou.aliyuncs.com/docker-org/jenkins:lts
3,������������
---
	sudo docker run --user root -itd -p 8080:8080 -p 50000:50000 --name jenkins -v /var/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock  registry.cn-hangzhou.aliyuncs.com/docker-org/jenkins:lts
4,������ɺ���Ĳ�������ַ
---
	vi /var/jenkins_home/hudson.model.UpdateCenter.xml
	#https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json
5,��������
---
	dockers restart ${����ID}
6,����127.0.0.0��8080
---
	�鿴��ʼ���룺 cat /var/jenkins_home/secrets/initialAdminPassword
