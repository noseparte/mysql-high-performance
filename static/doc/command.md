### MySQL的命令汇总


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