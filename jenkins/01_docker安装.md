1, 创建用户
---
	useradd jenkins
	usermod -g docker jenkins
2,创建挂载目录
---
	mkdir /var/jenkins_home
	chown -R 1000:1000 /var/jenkins_home
	chmod -R 777 /var/jenkins_home
3,下载镜像
---
	docker pull registry.cn-hangzhou.aliyuncs.com/docker-org/jenkins:lts
3,镜像启动命令
---
	sudo docker run --user root -itd -p 8080:8080 -p 50000:50000 --name jenkins -v /var/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock  registry.cn-hangzhou.aliyuncs.com/docker-org/jenkins:lts
4,启动完成后更改插件网点地址
---
	vi /var/jenkins_home/hudson.model.UpdateCenter.xml
	#https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json
5,重启容器
---
	dockers restart ${容器ID}
6,访问127.0.0.0：8080
---
	查看初始密码： cat /var/jenkins_home/secrets/initialAdminPassword
