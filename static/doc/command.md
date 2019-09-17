### MySQL的命令汇总


#### MySQL的基本操作语句

```mysql
# 查看全部数据库;
show databases;
# 切换数据库;
use qr_gs;
# 查看当前数据库
select database();
# 查看当前数据库下的所有表
show tables;
# 查看表结构
desc role;
# 查看表创建语句
show create table role;
# 查看表的所有数据
select * from role;
# 查看mysql的版本号
select version();
# 查看表的状态
show table status like 'role';
```

#### MySQL的事务

```mysql
START TRANSACTION;
SELECT balance FROM checking WHERE customer_id = 10233276;
UPDATE checking SET balance = balance-200.00 WHERE customer_id = 10233276;
UPDATE savings SET balance = balance+200.00 WHERE customer_id = 10233276;
COMMIT;
```

#### 查询MySQL的事务的隔离级别和mysql事务隔离级别修改
    
```mysql
# 查询MySQL的事务的隔离级别
SELECT @@global.transaction_isolation,@@transaction_isolation;
# mysql事务隔离级别修改
set global transaction isolation level read committed;
```    

#### 查询MySQL的事务日志
    
```mysql
# 查询MySQL的事务日志状态
show global variables like 'log_bin';
```    

#### 查询MySQL的事务自动提交
    
```mysql
# 查询MySQL是否开启事务自动提交
show variables like 'autocommit';
```    


#### MySQL复制表(CREATE AND SELECT) 
    
```mysql
# MySQL复制表
CREATE TABLE innodb_table LIKE myisam_table;
ALTER TABLE innodb_table ENGINE=INNODB;
INSERT INTO innodb_table SELECT * FROM myisam_table;

# 全量复制
START TRANSACTION;
INSERT INTO innodb_table SELECT * FROM myisam_table WHERE id BETWEEN x AND y;
COMMIT;
```    



#### MySQL慢查询日志 (slow_query_log)
    
```mysql
# MySQL慢查询是否开启
show global variables like '%slow_query_log%';
```    

