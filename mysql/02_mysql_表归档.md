1������һ���滻��ע�� create table like �� as ������
---
	#as����������ͬ��ṹ������Դ�����ݡ�ע�⣺��������ʵֻ�ǰ�select���Ľ����һ��������newadmin��� ������������������
	#like��������������ṹ��ȫ������
	#CREATE TABLE newadmin LIKE admin; 
	#INSERT INTO newadmin SELECT * FROM admin;
	create table t_bak like t;
2���޸� �滻�� ��id��ʼֵ
---
	�޸�id��ʼֵ����ʼֵ���ϱ�id��һ�� �������
	alter table t_bak AUTO_INCREMENT=10000;
3����������
---
	rename table t to t_his;
	rename table t_bak to t;
4,һ�����ӣ�
---
	-- �����ı� �鵵
	-- 1�������±�
	create table ST_SETTLEMENT_BASIS_ITEM_temp like ST_SETTLEMENT_BASIS_ITEM;
	create table ST_SETTLEMENT_SLIP_ITEM_temp like ST_SETTLEMENT_SLIP_ITEM;
	create table ST_SETTLEMENT_SLIP_temp like ST_SETTLEMENT_SLIP;
	create table ST_SETTLEMENT_TICKET_temp like ST_SETTLEMENT_TICKET;
	-- 2�������±�����
	ALTER TABLE ST_SETTLEMENT_BASIS_ITEM_temp ADD FOREIGN KEY (SETTLEMENT_TICKET_ID) REFERENCES ST_SETTLEMENT_TICKET_temp(ID);
	ALTER TABLE ST_SETTLEMENT_SLIP_ITEM_temp ADD FOREIGN KEY (SETTLEMENT_SLIP_ID) REFERENCES ST_SETTLEMENT_SLIP_temp(ID);
	ALTER TABLE ST_SETTLEMENT_SLIP_temp ADD FOREIGN KEY (SETTLEMENT_TICKET_ID) REFERENCES ST_SETTLEMENT_TICKET_temp(ID);
	-- rename �ϱ�
	rename table ST_SETTLEMENT_BASIS_ITEM to ST_SETTLEMENT_BASIS_ITEM_20181022_his;
	rename table ST_SETTLEMENT_SLIP_ITEM to ST_SETTLEMENT_SLIP_ITEM_20181022_his;
	rename table ST_SETTLEMENT_SLIP to ST_SETTLEMENT_SLIP_20181022_his;
	rename table ST_SETTLEMENT_TICKET to ST_SETTLEMENT_TICKET_20181022_his;
	-- rename �±�
	rename table ST_SETTLEMENT_BASIS_ITEM_temp to ST_SETTLEMENT_BASIS_ITEM;
	rename table ST_SETTLEMENT_SLIP_ITEM_temp to ST_SETTLEMENT_SLIP_ITEM;
	rename table ST_SETTLEMENT_SLIP_temp to ST_SETTLEMENT_SLIP;
	rename table ST_SETTLEMENT_TICKET_temp to ST_SETTLEMENT_TICKET;