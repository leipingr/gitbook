# Redis Sentinel ( Master-Slave )
-----------------

### Redis Sentinel集群方案

Redis Sentinel是Redis提供的一种高可用解决方案。Sentinel可理解是一种分布式系统或一套管理工具，它提供了三大核心功能：

* Master-Slave服务监控
* Master存活检测
* Failover自动化

Redis Sentinel仍基于M-S，本文将就此方案进行详细说明。
