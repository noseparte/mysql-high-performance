##### 1.3.2 死锁

死锁是指俩个或者多个事务在同一资源上相互占用,并请求锁定对方占用的资源，
从而导致恶性循环的现象。
当多个事务试图以不同的顺序锁定资源时，就可能产生死锁。
多个事务同时锁定一个资源时。也会产生死锁。

