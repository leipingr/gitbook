#配置Master实例
---

uchatMaster主机安装完redis产品后，可进行初步的配置。

### 1. 定义配置文件

重新定义Master实例的配置文件为： <font color=red>**uchatMaster.conf**</font>

```sh
$cd ~/redis-2.8.19
$cp redis.conf uchatMaster.conf
```

redis产品默认采用 **6379** 作为服务端口，这里也可不作修改，直接采用默认配置即可。

### 2. 参数配置项说明

redis配置内容有很多，包括数据库常用定义，持久化，主从关系，复制等参数。 系统默认配置可不做调整也可直接应用。

配置文件中英文注释己非常详细（这里只是将已用到的参数作下中文注释，暂时没有用到的或未理解的后面再补充）。配置项说明如下：

```sh

################################ GENERAL  #####################################

# 如果要将redis设置为从后台启动，应更改为yes
daemonize no

pidfile /var/run/redis.pid

# 设置redis的运行端口
port 6379

tcp-backlog 511

# 设置客户端连接时的超时时间（单位:s），当客户端这段时间内没有发出任何指令时关闭此连接，0 表示关闭此设置，不作检查。
timeout 0

tcp-keepalive 0

# 日志级别（debug/verbose/notice/warning）,生产环境建议使用notice
loglevel notice

logfile ""

# 可用数据库数，表示1个实例有16个数据库，数据库名分别为0〜15. 默认数据库为0
databases 16

################################ SNAPSHOTTING  ################################

# 持久化配置：指定多长时间内，有多少次更新操作，就将数据同步到数据文件rdb中。
save 900 1         //900秒内至少1个key被改变
save 300 10        //300秒内至少10个key被改变
save 60 10000      //60秒内至少10000个key被改变

stop-writes-on-bgsave-error yes

# 持久化到rdb文件时是否压缩数据
rdbcompression yes

rdbchecksum yes

# 本地持久化数据库文件名，默认是 dump.rdb
dbfilename dump.rdb

# 数据库镜像备份文件及临时文件暂存的路径。实际上就在目录 src/下
dir ./

################################# REPLICATION #################################

# 因为本机是Master, 故无需配置。具体可参考 "配置Slave实例" 说明
# slaveof <masterip> <masterport>

slave-serve-stale-data yes

slave-read-only yes

repl-diskless-sync no

repl-diskless-sync-delay 5

repl-disable-tcp-nodelay no

slave-priority 100


################################### LIMITS ####################################

# 并发数。0表示对客户端连接数不作限制。当同时打开的客户端连接数达到限制时，Redis会关闭新的连接并向客户端返回max number of clients.
# maxclients 10000

# redis最大内存限制。达到最大内存后，Redis会先尝试清除已到期或即将到期的key，并移除空的list对象，处理完后仍达到最大内存，将无法进行写操作，仍可进行读操作。
# maxmemory <bytes>

############################## APPEND ONLY MODE ###############################

# 即所说的AOF模式，该方式比rdb备份更高效。
appendonly no

appendfilename "appendonly.aof"

appendfsync everysec

no-appendfsync-on-rewrite no

auto-aof-rewrite-percentage 100
auto-aof-rewrite-min-size 64mb

aof-load-truncated yes

################################ LUA SCRIPTING  ###############################

lua-time-limit 5000

################################## SLOW LOG ###################################

slowlog-log-slower-than 10000

slowlog-max-len 128

################################ LATENCY MONITOR ##############################

latency-monitor-threshold 0

############################# Event notification ##############################

notify-keyspace-events ""

############################### ADVANCED CONFIG ###############################

hash-max-ziplist-entries 512
hash-max-ziplist-value 64

list-max-ziplist-entries 512
list-max-ziplist-value 64

set-max-intset-entries 512

zset-max-ziplist-entries 128
zset-max-ziplist-value 64

hll-sparse-max-bytes 3000

activerehashing yes

client-output-buffer-limit normal 0 0 0
client-output-buffer-limit slave 256mb 64mb 60
client-output-buffer-limit pubsub 32mb 8mb 60

hz 10

aof-rewrite-incremental-fsync yes
```

如上配置项均可根据实际需要灵活配置。
