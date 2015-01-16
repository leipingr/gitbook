# 配置Slave实例
---

uchatSlave主机安装完redis产品后，可以对Slave机进行相关配置。

### 1. 定义配置文件

重新定义Slave实例的配置文件为： <font color=red>**uchatSlave.conf**</font>

```sh
$cd ~/redis-2.8.19
$cp redis.conf uchatSlave.conf
```

uchatSlave由于采用其它的虚拟机，所以仍可采用默认 **6379** 作为服务端口。

### 2. 修改配置文件

编辑 uchatSlave.conf 配置文件，在注释**REPLICATION** 段**添加**如下内容，

```sh
slaveof 172.18.63.74 6379
```
其它配置项内容可完全与Master的配置一样。

### 3. Slave其它配置项说明

重要参数的说明如下：

```sh

################################# REPLICATION #################################

# 主从复制，当本机为slave时，需要配置master的IP地址和端口
slaveof 172.18.63.74 6379

# 当Slave同Master失去连接或复制正在进行时，Slave有两种运行方式：
# yes : Slave仍会继续响应客户端的请求
# no  : 除INFO和SLAVOF命令外，任何请求都会返回错误"SYNC with master in progress"
slave-serve-stale-data yes

# Slave为只读模式，即Master没有failover时，客户端不能对Slave进行写操作。
slave-read-only yes

repl-diskless-sync no

repl-diskless-sync-delay 5

repl-disable-tcp-nodelay no

slave-priority 100

min-slaves-max-lag 10
```

对于Slave实例而言，<font color=red>配置项 “slaveof 172.18.63.74 6379” 是必须的。</font>
