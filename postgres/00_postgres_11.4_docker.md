1,下载 docker 镜像
---
	docker push registry.cn-hangzhou.aliyuncs.com/docker-org/postgres:11.4
2,启动postgres
---
    mkdir -p /var/postgres/data
    sudo docker run -d -v /var/postgres/data:/var/lib/postgresql/data -p 5432:5432 -e 'POSTGRES_USER=root' -e 'POSTGRES_DB=database' -e 'POSTGRES_PASSWORD=123456' registry.cn-hangzhou.aliyuncs.com/docker-org/postgres:11.4
3,根据自己的需求修改 pg_hba.conf
---
	vi /var/postgres/data/pg_hba.conf
	#添加
	host    all             all             0.0.0.0/0               md5
4,通过工具测试连接
---