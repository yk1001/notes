1，创建一个替换表；注意 create table like 与 as 的区别
---
	#as用来创建相同表结构并复制源表数据。注意：这个语句其实只是把select语句的结果建一个表。所以newadmin这个 表不会有主键，索引。
	#like用来创建完整表结构和全部索引
	#CREATE TABLE newadmin LIKE admin; 
	#INSERT INTO newadmin SELECT * FROM admin;
	create table t_bak like t;
2，修改 替换表 的id起始值
---
	修改id起始值，起始值对老表id有一定 间隔冗余
	alter table t_bak AUTO_INCREMENT=10000;
3，表重命名
---
	rename table t to t_his;
	rename table t_bak to t;
4,一个栗子：
---
	-- 结算四表 归档
	-- 1，创建新表
	create table ST_SETTLEMENT_BASIS_ITEM_temp like ST_SETTLEMENT_BASIS_ITEM;
	create table ST_SETTLEMENT_SLIP_ITEM_temp like ST_SETTLEMENT_SLIP_ITEM;
	create table ST_SETTLEMENT_SLIP_temp like ST_SETTLEMENT_SLIP;
	create table ST_SETTLEMENT_TICKET_temp like ST_SETTLEMENT_TICKET;
	-- 2，创建新表的外键
	ALTER TABLE ST_SETTLEMENT_BASIS_ITEM_temp ADD FOREIGN KEY (SETTLEMENT_TICKET_ID) REFERENCES ST_SETTLEMENT_TICKET_temp(ID);
	ALTER TABLE ST_SETTLEMENT_SLIP_ITEM_temp ADD FOREIGN KEY (SETTLEMENT_SLIP_ID) REFERENCES ST_SETTLEMENT_SLIP_temp(ID);
	ALTER TABLE ST_SETTLEMENT_SLIP_temp ADD FOREIGN KEY (SETTLEMENT_TICKET_ID) REFERENCES ST_SETTLEMENT_TICKET_temp(ID);
	-- rename 老表
	rename table ST_SETTLEMENT_BASIS_ITEM to ST_SETTLEMENT_BASIS_ITEM_20181022_his;
	rename table ST_SETTLEMENT_SLIP_ITEM to ST_SETTLEMENT_SLIP_ITEM_20181022_his;
	rename table ST_SETTLEMENT_SLIP to ST_SETTLEMENT_SLIP_20181022_his;
	rename table ST_SETTLEMENT_TICKET to ST_SETTLEMENT_TICKET_20181022_his;
	-- rename 新表
	rename table ST_SETTLEMENT_BASIS_ITEM_temp to ST_SETTLEMENT_BASIS_ITEM;
	rename table ST_SETTLEMENT_SLIP_ITEM_temp to ST_SETTLEMENT_SLIP_ITEM;
	rename table ST_SETTLEMENT_SLIP_temp to ST_SETTLEMENT_SLIP;
	rename table ST_SETTLEMENT_TICKET_temp to ST_SETTLEMENT_TICKET;