# 单机无缝升级
---

如果要将现有单机升级为集群方式，并且尽可以减少影响性，实现无缝升级，主要操作步骤如下：

* 单机直接作为Master
* 挂载Slave
* 启动Sentinel监控服务
* 客户端需要更改调用方式
---

### 1. 单机直接作为uchatMaster

单机不更改任何配置，直接作为uchatMaster

### 2. 挂载Slave

为uchatMaster添加从机，主要包括如下具体步骤：

**在新机上重新安装与单机版本一致的redis产品，假定单机版本为2.8.19，则执行如下命令：**
```sh
$ tar xzf redis-2.8.19.tar.gz
$ cd redis-2.8.19
$ make
$ make test
```

**uchatSlave复制采用原单机的redis配置文件：**
```sh
$ scp sentinel.conf uchatredis@172.18.63.75:/home/uchatredis/redis-2.8.19/
$ mv sentinel.conf uchatSlave.conf
```

**修改配置文件uchatSlave.conf，假定单机的ip，port如下，添加配置：**
```sh
slaveof 172.18.63.74 6379
```

**启动uchatSlave从机：**
```sh
$cd ~/redis-2.8.19/src
$./redis-server ../uchatSlave.conf &
```

### 3. 启动Sentinel监控服务

直接参考“配置基本步骤” -> “1.4 配置Sentinel监控服务”

至此，就完成了产品的配置工作，接下来需要对调用客户端进行调整。

### 4. 客户端需要更改调用方式

为了做到对应用的透明，要调整下客户端的调用方式，以后应用将直接调用sentinel的IP及PORT。

Case Code如下：
```java
Set<String> sentinels = new HashSet<String>();
sentinels.add("172.18.63.110:26379");
JedisSentinelPool pool = new JedisSentinelPool("uchatMaster", sentinels);
Jedis jedis = pool.getResource();
jedis.set("name", "reifu");
pool.returnResource(jedis);
String value = jedis.get("name");
System.out.println("Value: " + value);
```
完成上述步骤后，就实现了单机向Sentinel集群方式（M-S）的升级。
