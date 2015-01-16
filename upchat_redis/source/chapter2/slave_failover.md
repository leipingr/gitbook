# Slave故障及恢复
---

验证uchatSlave宕机后的影响。

### uchatSlave宕机

实际上当uchatSlave宕机后，对客户端提供的服务不会有任何影响。因为此时uchatSentinel监控到的主Master没有改变，仍然是uchatMaster对外提供服务。

只是日志会提示从Slave已Shutdown。

```sh
[27593] 25 Jan 19:30:22.569 # +sdown slave 172.18.63.75:6379 172.18.63.75 6379 @ uchatMaster 172.18.63.74 6379
```

### uchatSlave重启

实际上当uchatSlave宕机后，对客户端提供的服务不会有任何影响。因为此时uchatSentinel监控到的主Master没有改变，仍然是uchatMaster对外提供服务。

```sh
[27732] 25 Jan 19:58:44.407 - 2 clients connected (0 slaves), 1747920 bytes in use
[27732] 25 Jan 19:58:49.420 - DB 0: 2 keys (0 volatile) in 4 slots HT.
[27732] 25 Jan 19:58:49.420 - 2 clients connected (0 slaves), 1747944 bytes in use
[27732] 25 Jan 19:58:52.543 - Accepted 172.18.63.75:46438
[27732] 25 Jan 19:58:52.543 * Slave 172.18.63.75:6379 asks for synchronization
[27732] 25 Jan 19:58:52.543 * Full resync requested by slave 172.18.63.75:6379
[27732] 25 Jan 19:58:52.543 * Starting BGSAVE for SYNC with target: disk
[27732] 25 Jan 19:58:52.545 * Background saving started by pid 28556
[28556] 25 Jan 19:58:52.552 * DB saved on disk
[28556] 25 Jan 19:58:52.553 * RDB: 6 MB of memory used by copy-on-write
[27732] 25 Jan 19:58:52.628 * Background saving terminated with success
[27732] 25 Jan 19:58:52.628 * Synchronization with slave 172.18.63.75:6379 succeeded
```
uchatSlave重启后，会自动加入到集群中。
