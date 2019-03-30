# booboo_mysql_advance
> MySQL 高级教程

[TOC]

**关于我：**不积跬步无以至千里，不积小流无以成江河。

**更新计划：**每周一个专题，不断完善。

## 入门要求

> 开始培训前，需要提前完成以下要求。

### 阿里云ACP认证考试

[阿里云大学ACP考试](https://edu.aliyun.com/certification)

基于阿里云核心产品技术分为云计算、大数据、云安全、人工智能、中间件几大领域，通过该认证证明您可以基于阿里云产品在对应的技术方向上解决企业的基本业务问题。

- ACA级别：助理工程师认证，获得此认证证明您可以进行阿里云基础产品的使用和管理。
- ACP级别：工程师认证，获得此认证证明您可以基于阿里云产品解决企业的基本业务问题。
- ACE级别：高级工程师认证，获得此认证证明您可以基于阿里云产品进行架构设计并解决业务发展中的主要问题。

必需先通过第一关ACP阿里云工程是认证。

### MySQL基本功

参加培训前请先给自己打分，【入门】包含十个项目，每个项目10分，如果满分，则可以进入培训，否则请先完成入门级的培训   ：

- [linux基础命令培训](https://github.com/BoobooWei/booboo_linux_base)
- [MySQL数据库初级培训](https://github.com/booboowei/booboo_mysql)
- 一、笔试题目 <https://www.wenjuan.in/s/JjAFVj/> 
  二、上机题目 
  基础部分 <https://cloudcare.itcloudlab.com/courses/sections/1d30ef9c010f47d1a3713c4de573c2aa/learning> 故障排查 <https://cloudcare.itcloudlab.com/courses/ed378f2a28e34b3aa8a07179b430c6ec/detail>



MYSQL入门：

- 会搭建主从复制？一主多从
- 了解最新的MGR集群
- 会编写增删该查的SQL
- 知道InnoDB行锁的不同语法
- 会用mysqldump进行数据库逻辑备份和恢复
- 会用perconaxtrabackup进行数据库物理备份和恢复
- 会使用Linux常用命令
- 会搭建LAMP架构的网站
- 会使用RDS数据库
- 会使用DTS迁移工具

## MySQL 高级教程培训

通过该培训教程能收获哪些？

### 总结能力

- 对每一个客户的落地需求，应提供相应的报告
- 报告建议使用MarkDown格式，Markdown编辑器推荐Typora <https://www.typora.io/> 非常轻量，适用于苹果、微软、Linux 有中文版本
- 报告输出为PDF交付客户
- 事件归类总结有自己的方法论（例如[常用故障排查命令](https://github.com/BoobooWei/DBA_Mysql/blob/master/%E5%B8%B8%E7%94%A8%E6%95%85%E9%9A%9C%E6%8E%92%E6%9F%A5%E5%91%BD%E4%BB%A41.txt)、[常用测试脚本](https://github.com/BoobooWei/DBA_Mysql/blob/master/%E5%B8%B8%E7%94%A8%E6%B5%8B%E8%AF%95%E8%84%9A%E6%9C%AC.txt)）
- Confluence总结归类按时输出

### 代码能力

- bash：能够编写自动备份恢复脚本（逻辑）、数据监控脚本
- python：能够使用现有的python应用发现、健康报告、故障自愈、慢查询报告等脚本
- sql：SQL调优

### 事件处理要求

- 生产环境中的操作必须事先在测试环境中验证通过，并将测试验证报告留档
- 钉钉及时响应，手机24小时开机

## 自我学习与沉淀

### 高阶

- 精通复制的原理
- 精通MHA的实现逻辑
- 精通MGR的机制
- 能对SQL进行调优
- 精通S、X、IS、IX锁的实现
- 精通mysqldump的实现原理

### 技术能力

- 熟知数据库各版本特性和Bug
- 解决难题的终极能力
- 拥有总结成方法论的能力
- 预测未来五年技术趋势的能力

### 业务能力

- 熟知各个业务在数据库侧的难点和解决之道
- 懂业务，能够协调业务一起进行架构改造
- 敢担责，勇背锅的能力

### 推荐书籍

#### 工作效率

推荐大家一本书，著名的搞定系列《Getting Things Done》的《搞定1无压工作的艺术》（GTD的已经成为时间管理系统的代称），这本书主要讲工作流程管理，个人效率提升方法，非常简单易行。GTD时间管理，并非是去管理时间，而是运用技巧、方法和工具帮助人们完成工作，实现目标，有效的运用时间。

* GTD的核心理念概括就是必须记录下来要做的事，然后整理安排并使自己一一去执行。
* GTD的五个核心原则是：收集、整理、组织、回顾、执行。
* GTD的核心理念在于清空大脑，然后一步步按照设定的路线去努力执行。

微信读书里有电子版的

#### MySQL的使用相关书籍

1. MySQL技术内幕InnoDB存储引擎
2. MySQL的官方手册
3. MySQL排错指南
4. 高性能MySQL
5. 数据库索引设计与优化
6. Effective MySQL系列

#### MySQL的源码相关书籍

1. InnoDB - A journey to the core
2. 深入MySQL源码
3. 深入理解MySQL核心技术
4. MySQL内核InnoDB存储引擎
5. MySQL Internals Manual
6. MariaDB原理与实现


## 培训专题预览

### Advice Class

>  咨询类

###  Action Class

> 操作类

| Action Class 操作类 | 进展   |
| ------------------- | ------ |
| 数据库安装配置      | [数据库安装配置](ActionClass/DatabaseInstallationConfiguration) |
| 数据库监控部署      | 未开始 |
| 数据库数据归档      | 未开始 |
| 数据库备份恢复      | 未开始 |

### Failure Class

>  故障类

| Failure Class 故障类 | 进展   |
| -------------------- | ------ |
| CPU故障              | 未开始 |
| IO故障               | 未开始 |
| 内存故障             | 未开始 |
| 磁盘故障             | 未开始 |
| 连接数故障           | 未开始 |
| 行锁故障             | 未开始 |
| 元锁故障             | 未开始 |
| 字符集故障           | 未开始 |
| 死锁故障             | 未开始 |



### Rescue Class

>  救援类

| Rescue Class 救援类      | 进展   |
| ------------------------ | ------ |
| 密码在线破解             | 未开始 |
| 数据库人为误操作数据恢复 | 未开始 |



### Migration Class

> 迁移类

| Migration Class 迁移类 | 进展   |
| ---------------------- | ------ |
| 同构数据库迁移         | 未开始 |
| 异构数据库迁移         | 未开始 |



### Optimize Class

> 优化类

| Optimize Class 优化类 | 进展   |
| --------------------- | ------ |
| SQL优化               | 未开始 |
| 架构优化              | 未开始 |



### Development Class

> 开发类

| Development Class 开发类 | 进展   |
| ------------------------ | ------ |
| 数据库建模               | 未开始 |
| 数据库自动化运维工具开发 | 未开始 |
| 大数据开发               | 未开始 |



### Explore Class

> 探索类

| Explore Class 探索类                             | 进展   |
| ------------------------------------------------ | ------ |
| RDS For MySQL 5.7 到IDC机房自建MySQL主从搭建研究 | 未开始 |
| 大表删除方案研究                                 | 未开始 |

