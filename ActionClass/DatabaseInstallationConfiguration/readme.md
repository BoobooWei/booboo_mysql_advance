<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [数据库安装配置](#数据库安装配置)
	- [规范](#规范)
		- [资源存储](#资源存储)
		- [脚本库、软件安装规范](#脚本库软件安装规范)
	- [安装文档](#安装文档)

<!-- /TOC -->

# 数据库安装配置

## 规范

### 资源存储

运维环境安装配置所需的源码、安装包、插件等统一存放至运维oss中。

相应的脚本、程序、代码统一存放至gitlab中，脚本wget oss中的源码完成安装。

### 脚本库、软件安装规范

相应环境安装配置，统一采用gitlab中脚本完成，包含系统初始化、系统配置等。

数据库安装部署脚本需求，对接到DBA组，DBA组需要至多一个工作日内提供安装脚本（特殊复杂软件脚本除外），上传至gitlab中。

## 安装文档

> 更新时间：2019-04-01

| 架构        | MySQL 分支                 | 最新版本 | 文档                                                         | 脚本                                 |
| ----------- | -------------------------- | -------- | ------------------------------------------------------------ | ------------------------------------ |
| Node        | MariaDB                    | 10.2.23  | [MariaDB单节点安装](install_doc/MariaDB.md)                  | [MariaDB二进制安装](install_script/) |
|             | MySQL                      | 8.0.15   | [MySQL单节点安装](install_doc/MySQL.md)                      | [MySQL二进制安装](install_script/)   |
|             | PerconaServer For MySQL    | 8.0.15   | [PerconaServer官方帮助文档](<https://www.percona.com/doc/percona-server/LATEST/index.html>) | [Percona二进制安装](install_script/) |
|             | Aliyun RDS For MySQL       | 5.7      | [RDS For MySQL官方帮助文档](<https://help.aliyun.com/document_detail/67687.html?spm=a2c4g.11186623.6.542.7385e2e0ZxrDzM>) |                                      |
|             | AWS RDS For MySQL          | 8.0      | [AWS RDS For MySQL官方帮助文档](<https://docs.amazonaws.cn/AmazonRDS/latest/UserGuide/USER_UpgradeDBInstance.MySQL.html>) |                                      |
|             | QCloud TencentDB for MySQL | 5.7      | [TencentDB For MySQL官方帮助文档](<https://cloud.tencent.com/document/product/236/30969>) |                                      |
|             | UCloud UDB-MySQL           | 5.6      | [UDB-MySQL官方帮助文档](<https://www.ucloud.cn/site/product/udb.html>) |                                      |
|             | 分支压力测试               |          | [单节点压力测试文档](sysbench/)                              | [压测脚本](install_script/)          |
| Replication | 半同步复制                 |          |                                                              |                                      |
|             | MySQL主从+Consul           |          | 自动故障转移                                                 |                                      |
|             | MHA+keepalived             |          | 自动故障转移+主从自动重构                                    |                                      |
| Cluster     | MySQL MGR                  |          | 组复制                                                       |                                      |
|             | Percona Xtra Cluter        |          | 集群                                                         |                                      |
|             |                            |          |                                                              |                                      |
