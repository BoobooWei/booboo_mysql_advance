<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [概述](#概述)
- [部署方式](#部署方式)
- [软件说明](#软件说明)
	- [软件版本说明](#软件版本说明)
	- [软件下载地址](#软件下载地址)
- [前提条件](#前提条件)
	- [配置](#配置)
- [依赖关系包](#依赖关系包)
- [安装步骤](#安装步骤)
	- [在线安装_在RedHat上安装](#在线安装在redhat上安装)
		- [使用yum（推荐）](#使用yum推荐)
			- [1 查看MariaDB Server版本](#1-查看mariadb-server版本)
			- [2 Yum安装MariaDB Server](#2-yum安装mariadb-server)
			- [3 查看软件架构](#3-查看软件架构)
	- [在线安装_在Ubuntu上安装](#在线安装在ubuntu上安装)
		- [1 导入GnuPG签名密钥](#1-导入gnupg签名密钥)
		- [2 新钥匙](#2-新钥匙)
		- [3 将MariaDB添加到sources.list](#3-将mariadb添加到sourceslist)
		- [4 使用apt-get安装MariaDB](#4-使用apt-get安装mariadb)
	- [离线安装_二进制手动安装](#离线安装二进制手动安装)
		- [1 下载二进制文件](#1-下载二进制文件)
		- [2 解压文件到安装路径](#2-解压文件到安装路径)
		- [3 确保二进制文件位于PATH环境变量中列出的目录中。](#3-确保二进制文件位于path环境变量中列出的目录中)
- [配置步骤](#配置步骤)
	- [在线源YUM安装的启动方式](#在线源yum安装的启动方式)
- [启动数据库](#启动数据库)
- [停止数据库](#停止数据库)
- [重启数据库](#重启数据库)
	- [在线源DEB安装的启动方式](#在线源deb安装的启动方式)
- [启动数据库](#启动数据库)
- [停止数据库](#停止数据库)
- [重启数据库](#重启数据库)
	- [二进制包安装的启动方式](#二进制包安装的启动方式)
		- [自动启动mysqld](#自动启动mysqld)
		- [安装后](#安装后)
- [验证](#验证)

<!-- /TOC -->

# 概述

MariaDB Server是一个安全，高度可用且可扩展的关系数据库服务器，具有现代，可扩展的架构，可促进创新。结合熟悉的SQL接口和开放的可扩展性，MariaDB通过提供稳定且可配置的数据层来支持创新，以覆盖广泛的用例，同时将熟悉的SQL接口与开放的可扩展性相结合。

MariaDB：MySQL的直接替代品

* MariaDB被设计为MySQL（R）的直接替代品，具有更多功能，新存储引擎，更少的错误和更好的性能。
* MariaDB由MariaDB Foundation带给您。请阅读CREDITS文件，了解有关MariaDB Foundation的详细信息，以及正在开发MariaDB的人员。
* MariaDB由MySQL的许多原始开发人员开发，他们现在为MariaDB Foundation和MariaDB Corporation以及社区中的许多人工作。
* MySQL是MariaDB的基础，是Oracle Corporation.Inc的产品和商标。


# 部署方式

官方帮助文档：https://mariadb.com/kb/en/library/getting-installing-and-upgrading-mariadb/

本文分别介绍了在线和离线两种环境下的安装的方式：

* 在线安装: 直接通过在线源进行安装
* 离线安装：在无法访问外网的情况下
    - 离线安装包
    - 二进制安装包
    - 源码编译安装

**安装方式的选择：**

* 如果可以在线安装则直接使用官方的源即可快速部署；
* 如果为离线安装，则所有的安装包（源码包、二进制预编译包、rpm包、deb包）都需要提前下载并拷贝到待安装服务器上。
* 由于源码编译安装需要非常熟悉软件的调优参数，除非定制，一般不建议选择源码编译安装；
* 离线安装包（rpm包、deb包）的方式不适用于多环境规范化部署，因此生产中也不建议使用；

**生产环境中，为了多环境部署的规范性，建议使用离线安装之二进制安装包。**

# 软件说明

## 软件版本说明

* 操作系统：RedHat 7.2  
* MairaDB：5.5

## 软件下载地址

本软件及依赖软件的下载地址，包括：

* 官方软件源：https://mariadb.com/kb/en/library/distributions-which-include-mariadb/
* 二进制包：https://downloads.mariadb.org/

# 前提条件

## 配置

如果您使用SELinux，则必须配置SELinux以允许MariaDB在基于Red Hat Linux的系统（Red Hat Enterprise Linux或CentOS Linux）上启动。

要配置SELinux，管理员有三个选项：

1. 如果SELinux处于enforcing模式，则启用对MariaDB部署将使用的相关端口的访问（例如3600）。对于默认设置，可以通过运行来完成

    ```shell
    semanage port -a -t mongod_port_t -p tcp 3600
    ```

2. 通过将SELINUX设置设置为disabled来 禁用SELinux，修改配置/etc/selinux/config。

    ```shell
    SELINUX =disabled
    ```

    必须重新引导系统才能使更改生效。

3. 通过将将SELinux设置为permissive模式。/etc/selinux/config

    ```shell
    SELINUX=permissive
    ```

    必须重新引导系统才能使更改生效。

    您可以改为使用setenforce更改为permissive模式。 setenforce不需要重新启动但不是持久性的。或者，您可以选择在安装Linux操作系统时不安装SELinux软件包，或选择删除相关软件包。此选项是最具侵入性的，不建议使用。

# 依赖关系包

安装必要的软件包：

```shell
yum install -y vim net-tools wget
```

# 安装步骤

## 在线安装_在RedHat上安装

使用本教程使用.rpm 软件包在Red Hat Enterprise Linux或CentOS Linux版本6和7上安装Mariadb Server 5.5。

> 平台支持
>
> 从RedHat7.0开始，系统自带的Yum源包含了MariaDB数据库源。

### 使用yum（推荐）

|项目|	参数|
|:--|:--|
|软件名|	mariadb-server 5.5|
|service|	mariadb|
|daemon|	mysqld|
|配置文件	|/etc/my.cnf /etc/my.cnf.d/*.cnf|
|数据文件|	/var/lib/mysql|
|日志文件|	/var/log/mariadb/mariadb.log（错误日志，启动日志）|
|端口号|	3306 |

#### 1 查看MariaDB Server版本

`yum list|grep mariadb`

#### 2 Yum安装MariaDB Server
`yum install -y mariadb-server`

#### 3 查看软件架构

`rpm -ql mariadb-server`


## 在线安装_在Ubuntu上安装
使用本教程在LTS Ubuntu Linux系统上安装Mariadb Server 5.5。

对于Debian和Ubuntu，强烈建议从仓库安装，使用apt-get，aptitude，synaptic包管理器。

设置内容的最简单方法是使用MariaDB的在线 [存储库配置工具](http://downloads.mariadb.org/mariadb/repositories/) 并按照其生成的说明进行操作。

### 1 导入GnuPG签名密钥

首先导入我们用于签署存储库的GPG密钥。此步骤只需在给定服务器上执行一次。密钥可以 apt验证它下载的软件包的完整性。

我们的签名密钥的ID是`0xcbcb082a1bb943db`，完整的密钥指纹是：

`1993 69E5 404B D5FC 7D2F E43B CBCB 082A 1BB9 43DB`
该apt-key应用程序是一种将此密钥导入apt的简单方法：

`sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db`

在Ubuntu或Debian系统上导入签名密钥时。导入命令保持不变。

例：

```shell
Example:
localhost:~# apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db
Executing: gpg --ignore-time-conflict --no-options --no-default-keyring --secret-keyring /tmp/tmp.ASyOPV87XC --trustdb-name /etc/apt/trustdb.gpg --keyring /etc/apt/trusted.gpg --primary-keyring /etc/apt/trusted.gpg --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db
gpg: requesting key 1BB943DB from hkp server keyserver.ubuntu.com
gpg: key 1BB943DB: "MariaDB Package Signing Key <package-signing-key@mariadb.org>" imported
gpg: no ultimately trusted keys found
gpg: Total number processed: 1
gpg:               imported: 1
```


添加密钥后，您就可以添加相应的存储库了。

### 2 新钥匙
在Debian 9“stretch”之后，dirmngr需要在导入密钥之前安装软件包：

```shell
sudo apt install dirmngr
```

截至Ubuntu 16.04“Xenial”，Debian 9“stretch”和Debian Sid，我们的签名密钥已经改变。新签名密钥的ID是`0xF1656F24C74CD1D8`，完整密钥指纹是：

`177F 4010 FE56 CA33 3630 0305 F165 6F24 C74C D1D8`
可以使用以下方式导入此新密钥apt-key：

```shell
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
```

旧密钥仍用于以前版本的Ubuntu和Debian。如果对您需要哪个键有疑问，那么导入两个键是完全安全的。

### 3 将MariaDB添加到sources.list
要轻松生成相应的sources.list条目（也称为APT行），请使用我们的在线 [存储库配置工具](http://downloads.mariadb.org/mariadb/repositories/)。

在该工具中，根据您使用的分发版选择“debian”或“ubuntu”，然后选择特定版本，然后选择要安装的MariaDB版本。例如，以下是使用主MariaDB镜像和Ubuntu 14.04“可信” 添加[MariaDB 10.0](https://mariadb.com/kb/en/what-is-mariadb-100/)存储库的说明：

```shell
udo apt-get install software-properties-common
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db
sudo add-apt-repository 'deb http://ftp.osuosl.org/pub/mariadb/repo/10.0/ubuntu trusty main'
```

您可以找到您正在使用的版本：

```
lsb_release -a
```

获得sources.list条目后，将它们添加到本地 /etc/apt/sources.list （例如使用“ sudo gedit /etc/apt/sources.list ”）或添加到单独的文件下sources.list.d/ （例如使用“ sudo gedit /etc/apt/sources.list.d/mariadb.list ”）。

您还可以使用“软件源”工具添加APT行。该工具位于“Ubuntu软件中心”的“编辑”菜单下。在“Synaptic”软件包管理器中，此工具称为“存储库”，它位于“设置”菜单下。启动工具后，选择“其他软件”选项卡，单击“添加...”按钮并粘贴到APT行（两行中的每一行一次）。

与添加GPG密钥一样，此步骤只需在给定服务器上执行一次。

### 4 使用apt-get安装MariaDB
使用密钥和APT线路，您现在可以运行：

```shell
sudo apt-get update
```

然后可以使用您最喜欢的包管理器安装MariaDB，例如：

```shell
sudo apt-get install mariadb-server
```

## 离线安装_二进制手动安装
在下面的示例中，我们在/usr/local/mysql目录中安装MariaDB （这是许多平台上MariaDB的默认位置）。但是任何其他目录也应该起作用。

### 1 下载二进制文件

[二进制文件](http://downloads.askmonty.org/)

### 2 解压文件到安装路径

在`/ usr / local / mysql`中以root身份安装MariaDB

如果您具有对系统的root访问权限，则可能需要在用户和组'mysql'下安装MariaDB（以保持与MySQL安装的兼容性）：

```shell
groupadd mysql
useradd -g mysql mysql
cd /usr/local
tar -zxvpf /path-to/mariadb-VERSION-OS.tar.gz
ln -s mariadb-VERSION-OS mysql
cd mysql
./scripts/mysql_install_db --user=mysql
chown -R root .
chown -R mysql data
```

`ln -s `建议使用符号链接，因为它可以同时轻松安装许多MariaDB版本（便于测试，升级，降级等）。

### 3 确保二进制文件位于PATH环境变量中列出的目录中。
修改`$PATH`，以便可以调用[mysql](https://mariadb.com/kb/en/mysql-client/),[mysqldump](https://mariadb.com/kb/en/mysqldump/)等客户端。

修改`.bashrc`或`.bash_profile`以使其永久化。

```
export PATH=$PATH:/usr/local/mysql/bin/
```

# 配置步骤

## 在线源YUM安装的启动方式

如果是通过在线源YUM安装，则无需配置直接启动数据库

```shell
# 启动数据库
systemctl start mariadb
# 停止数据库
systemctl stop mariadb
# 重启数据库
systemctl restart mariadb
```

## 在线源DEB安装的启动方式

如果是通过在线源YUM或者DEB安装，则无需配置直接启动数据库

```shell
# 启动数据库
sudo service mongod start
# 停止数据库
sudo service mongod stop
# 重启数据库
sudo service mongod restart
```

## 二进制包安装的启动方式

### 自动启动mysqld

您可以通过将文件`mysql.server`文件复制到正确的位置来使`mysqld`（MariaDB服务器）自动启动。

```
cp support-files/mysql.server /etc/init.d/mysql.server
systemctl start mysql
```

### 安装后

在此之后，请记住为可从不受信任的来源访问的所有帐户设置正确的密码，以避免让主机面临安全风险！也可以考虑使用的[mysql.server](https://mariadb.com/kb/en/mysqlserver/)到 [自动启动MariaDB](https://mariadb.com/kb/en/starting-and-stopping-mariadb-automatically/)的 ，当你的系统启动。

我们的MariaDB二进制文件类似于可用于MySQL二进制分发的通用二进制文件。因此，有关使用这些二进制文件的更多选项，可以参考有关[安装通用二进制文件](http://docs.oracle.com/cd/E17952_01/refman-5.5-en/binary-installation.html)的MySQL 5.5手册条目 。

有关用于构建二进制文件的确切步骤的详细信息，请参阅KB 的 [编译MariaDB部分](https://mariadb.com/kb/en/compiling-mariadb-from-source/)。



# 验证
执行到这一步能够成功将服务启动，通过mysql客户端工具访问本地的MariaDB服务即可。

查看后台进程是否启动 `ps -ef|grer mysql`

查看监听端口是否启动 `ss -luntp | grep mysql`

客户端登陆方式：`mysql`

```shell
[root@mastera0 ~]# ps -ef|grep mysqld
mysql     2496     1  0 13:56 ?        00:00:00 /bin/sh /usr/bin/mysqld_safe --basedir=/usr
mysql     2653  2496  0 13:56 ?        00:00:00 /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --log-error=/var/log/mariadb/mariadb.log --pid-file=/var/run/mariadb/mariadb.pid --socket=/var/lib/mysql/mysql.sock
root      2694  2347  0 13:56 pts/0    00:00:00 grep --color=auto mysqld
[root@mastera0 ~]# netstat -luntp|grep mysqld
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN      2653/mysqld
```
