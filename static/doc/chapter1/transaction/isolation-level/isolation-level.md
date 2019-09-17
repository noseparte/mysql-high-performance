##### 1.3.1 隔离级别

隔离性其实比想象的更复杂。
在SQL标准中定义了四种隔离级别，每一种级别都规定了一个事务中所做的修改，
那些在事务内和事务间是可见的，哪些是不可见的。
较低级别的隔离通常可以执行更高的并发，系统的开销也更低。

下面简单地介绍一下四种隔离级别：

> READ UNCOMMITTED (未提交读)

    在**READ UNCOMMITTED**级别，事务中的修改，
    即使没有提交，对其他事务也都是可见的。
    事务可以读取未提交的数据，这也被称为脏读(Dirty Read)。
    这个级别会导致很多问题，从性能上来说，READ UNCOMMITTED不会比其他的级别好太多，
    但却缺乏其他级别的很多好处，除非真的有非常必要的理由，在实际应用中一般很少使用。
    
> READ COMMITTED (提交读)

    大多数数据库系统的默认隔离级别都是READ COMMITTED(但MySQL不是)。
    READ COMMITTED满足前面提到的隔离性的简单定义：一个事务开始时，只能“看见”已经提交的事务所做的秀爱。
    换句话说，一个事务从开始知道提交之前，所做的任何修改对其他事务都是不可见的。
    这个级别有时候也叫作不可重复读(nonrepeatable read),因为俩次执行同样的查询，可能会得到不一样的结果。
    
> REPEATABLE READ (可重复读)

    REPEATABLE READ 解决了脏读的问题。该级别保证了再同一个事务中多次读取同样记录的结果是一致的。
    但是理论上，可重复读隔离级别还是无法解决另外一个幻读(Phantom Read)的问题。
    所谓幻读，指的是当某个事务在读取某个范围的记录时，
    另外一个事务又在该范围内插入了新的记录，当之前的事务再次读取该范围的记录时，会产生幻行(Phantom Row)。
    InnoDB和XtraDB存储引擎通过多版本并发控制(MVCC，Multiversion Concurrency Control)解决了幻读的问题。
    可重复读是MySQL的默认事务隔离级别。
    
> SERIALIZABLE (可串行化)

    SERIALIZABLE 是最高的隔离级别。
    它通过强制事务串行执行，避免了前面说的幻读的问题。
    简单来说，SERIALIZABLE会在读取的每一行数据上都加锁，所以可能导致大量的超时和锁争用的问题。
    实际应用中也很少用到这个隔离级别，只有在非常需要确保数据的一致性而且可以接受没有并发的情况下，才考虑采用该级别。
    
- 表1-1： ANSI SQL隔离级别

| 隔离级别 | 脏读可能性 | 不可重复读可能性 | 幻读可能性 | 加锁读  |
| :-----: | :-------: | :------------: | :------: | :-----: |   
|READ UNCOMMITTED | Yes | Yes | Yes | No |
|READ COMMITTED | No | Yes | Yes | No |
|REPEATABLE READ  | No | No | Yes | No |
|SERIALIZABLE | No | No | No | Yes |
    
    
> 补充： 查询MySQL的事务的隔离级别和mysql事务隔离级别修改
    
```mysql
# 查询MySQL的事务的隔离级别
SELECT @@global.transaction_isolation,@@transaction_isolation;
# mysql事务隔离级别修改
set global transaction isolation level read committed;
```    