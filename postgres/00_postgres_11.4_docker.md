1,���� docker ����
---
	docker push registry.cn-hangzhou.aliyuncs.com/docker-org/postgres:11.4
2,����postgres
---
    mkdir -p /var/postgres/data
    sudo docker run -d -v /var/postgres/data:/var/lib/postgresql/data -p 5432:5432 -e 'POSTGRES_USER=root' -e 'POSTGRES_DB=database' -e 'POSTGRES_PASSWORD=123456' registry.cn-hangzhou.aliyuncs.com/docker-org/postgres:11.4
3,�����Լ��������޸� pg_hba.conf
---
	vi /var/postgres/data/pg_hba.conf
	#���
	host    all             all             0.0.0.0/0               md5
4,ͨ�����߲�������
---