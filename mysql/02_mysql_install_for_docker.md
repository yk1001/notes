1,���عٷ�docker
---
    docker pull mysql:8.0
    #docker pull registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
    #docker pull registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:5.7
    #docker pull registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:5.6
2,��������Ŀ¼
---
    mkdir -p /var/mysql/conf
    mkdir -p /var/mysql/data
3,��Ŀ¼/var/mysql/conf �����ļ� config-file.cnf
---
    [mysqld]
    #�������������
    max_connections=200
    #�����ʹ�õ��ַ���Ĭ��Ϊ8���ر����latin1�ַ���
    character-set-server=utf8
    #�����±�ʱ��ʹ�õ�Ĭ�ϴ洢����
    default-storage-engine=INNODB
    default-authentication-plugin=mysql_native_password
    sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
4,����docker images
---
    sudo docker run --name mysql -v /var/mysql/conf:/etc/mysql/conf.d -v /var/mysql/data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d registry.cn-hangzhou.aliyuncs.com/docker-org/mysql:8.0
    #/etc/mysql/conf.d �Ǿ�����Ĭ���Զ��������ļ��ĵ�ַ�����ļ������ûḲ�� my.cnfĬ������
    #/var/lib/mysql �Ǿ�����Ĭ��datadirĿ¼
5,��֤
---
    navicat �������ͻ��� ����������֤
    ls -a /var/mysql/data #����Ŀ¼������֤