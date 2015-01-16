> 中国银联 | 技术开发中心 | 公共组件室 ：[雷平](mailto:leiping@unionpay.com)


# 关于 Redis
-----------------

Redis（ http://redis.io ）是一个开源、支持网络、基于内存、键值对存储的数据库，它使用ANSI C语言编写。Redis是最流行的键值对存储数据库之一。

### <font color=blue>强大之处在于：</font>

- Redis中值的类型不仅限于字符串，还支持list，hash等抽象数据类型
- 可作为缓存也支持永久性存储，并支持多种持久化方式
- 拥有出色的读写性能，对于高并发的情形较适合


     基本功能使用可参考官方网站：http://redis.io


# Redis 高可用解决方案 ####

###简单容灾备份方案

对于Redis而言，其实最简单的容灾方案即是Master-Slave主从式架构。

 - 1个master可以有多个slave，在slave的conf文件中增加slaveof <masterip>  <masterport>即可
 - 在slave启动时，会自动从master同步数据到slave
 - 如果slave没有在运行，则会在下次slave启动时自动同步最新

<font color=red>但最大的缺点是</font> ：当Master宕机后，Slave不能自动接管，客户端调用需要切换到Slave的IP地址。

###[Redis集群方案](http://redis.io/topics/sentinel)

为了解决集群及对客户端透明的问题，较多人采用如下3种方案实现：

* 采用Keepalived实现集群
* 采用Zookeeper实现集群
* 采用Sentinel实现集群

由于前2种均需要额外安装其它软件，这里暂时不作研究。
对于Redis 2.8以上的版本，Redis的作者提供了Sentinel工具作为类似的高可用的解决方案。

这里将主要介绍Redis Sentinel是如何实现高可用的。




