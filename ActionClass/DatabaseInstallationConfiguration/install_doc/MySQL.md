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
		- [添加MySQL Yum源](#添加mysql-yum源)
		- [选择5.7系列](#选择57系列)
		- [安装MySQL Server 5.7](#安装mysql-server-57)
	- [在线安装_在Ubuntu上安装](#在线安装在ubuntu上安装)
		- [添加MySQL APT源](#添加mysql-apt源)
		- [使用APT安装MySQL](#使用apt安装mysql)
	- [离线安装_二进制手动安装](#离线安装二进制手动安装)
		- [安装依赖包](#安装依赖包)
		- [下载二进制文件](#下载二进制文件)
		- [MySQL安装布局](#mysql安装布局)
		- [创建一个mysql用户和组](#创建一个mysql用户和组)
		- [解压缩二进制安装包](#解压缩二进制安装包)
		- [确保二进制文件位于`PATH`环境变量中列出的目录中。](#确保二进制文件位于path环境变量中列出的目录中)
- [配置步骤](#配置步骤)
	- [在线源YUM安装的启动方式](#在线源yum安装的启动方式)
	- [在线源DEB安装的启动方式](#在线源deb安装的启动方式)
	- [二进制包安装的启动方式](#二进制包安装的启动方式)
		- [自动启动mysqld](#自动启动mysqld)
		- [安装后](#安装后)
- [验证](#验证)

<!-- /TOC -->
# 概述

MySQL 是采用客户/服务器模型的开放源码关系型 SQL 数据库管理系统,它 可以在多种操作系统上运行,它是由 MySQL Ab 公司开发、发布并支持的，后被sun收购，现在在oracle公司旗下，知名的分支MariaDB，Percona Server。

# 部署方式

> 官方帮助文档：[https://dev.mysql.com/doc/refman/5.7/en/installing.html](https://dev.mysql.com/doc/refman/5.7/en/installing.html)

本文分别介绍了在线和离线两种环境下的安装的方式，即：

1.  在线安装
2.  离线安装
    1.  离线安装包
    2.  二进制安装包
    3.  源码编译安装

安装方式的选择：

1.  如果可以在线安装则直接使用官方的源即可快速部署；如果为离线安装，则所有的安装包（源码包、二进制预编译包、rpm包、deb包）都需要提前下载并拷贝到待安装服务器上。
2.  由于源码编译安装需要非常熟悉软件的调优参数，除非定制，一般不建议选择源码编译安装；
3.  离线安装包（rpm包、deb包）的方式不适用于多环境规范化部署，因此生产中也不建议使用；
4.  生产环境中，为了多环境部署的规范性，建议使用离线安装之二进制安装包。

# 软件说明

## 软件版本说明

*   操作系统：RedHat 7.2
*   MySQL：5.7.17

## 软件下载地址

本软件及依赖软件的下载地址，包括：

*   官方软件源：[https://dev.mysql.com/doc/refman/5.7/en/linux-installation.html](https://dev.mysql.com/doc/refman/5.7/en/linux-installation.html)
*   二进制包：[https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.24-linux-glibc2.12-x86_64.tar](https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.24-linux-glibc2.12-x86_64.tar)

# 前提条件

## 配置

如果您使用SELinux，则必须配置SELinux以允许MySQL在基于Red Hat Linux的系统（Red Hat Enterprise Linux或CentOS Linux）上启动。

要配置SELinux，管理员有三个选项：

* 如果SELinux处于`enforcing`模式，则启用对MariaDB部署将使用的相关端口的访问（例如`3600`）。对于默认设置，可以通过运行来完成

    ```shell
    semanage port -a -t mongod\_port\_t -p tcp 3600
    ```

* 通过将`SELINUX`设置设置为`disabled`来 禁用SELinux `/etc/selinux/config`。

    ```shell
    SELINUX =disabled
    ```

    必须重新引导系统才能使更改生效。  


* 通过将将SELinux设置为`permissive`,设置`/etc/selinux/config`

    ```shell
    SELINUX=permissive
    ```

    必须重新引导系统才能使更改生效。

    您可以改为使用`setenforce`更改为`permissive`模式。 `setenforce`不需要重新启动但不是持久性的。或者，您可以选择在安装Linux操作系统时不安装SELinux软件包，或选择删除相关软件包。此选项是最具侵入性的，不建议使用。


## 依赖关系包

安装必要的软件包：

```shell
yum install -y vim net-tools wget yum-utils
```

# 安装步骤

## 在线安装_在RedHat上安装

使用本教程使用`.rpm` 软件包在Red Hat Enterprise Linux或CentOS Linux版本6和7上安装MySQL Server 5.7.24 。

| 项目 | 参数 |
| ---- | ---- |
|软件名|mysql-community-server|
|service|mysql|
|daemon|mysqld|
|配置文件|/etc/my.cnf  /etc/my.cnf.d/*.cnf|
|数据文件|/var/lib/mysql|
|日志文件|/var/log/msyqld.log（错误日志，启动日志）|
|端口号|3306|

### 添加MySQL Yum源

```bash
wget "https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm"
yum localinstall -y mysql80-community-release-el7-1.noarch.rpm
```

### 选择5.7系列

```bash
yum-config-manager --disable mysql80-communityyum-config-manager --enable mysql57-community
```

### 安装MySQL Server 5.7

```bash
yum install mysql-community-server -y
```

这将安装MySQL server（`mysql-community-server`）的包以及运行服务器所需组件的包，包括client（`mysql-community-client`）的包，客户端和服务器的常见错误消息和字符集（`mysql-community-common`）以及共享客户端库（`mysql-community-libs`） 。

## 在线安装_在Ubuntu上安装

使用本教程在LTS Ubuntu Linux系统上安装MySQL Server 5.7.24。

对于Debian和Ubuntu，强烈建议从仓库安装，使用`apt-get`，`aptitude`，`synaptic`包管理器。

官方帮助文档[https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/)

### 添加MySQL APT源

```bash
sudo wget "https://dev.mysql.com/get/mysql-apt-config\_0.8.10-1\_all.deb"
sudo dpkg -i mysql-apt-config\_0.8.10-1\_all.deb
```

### 使用APT安装MySQL

```bash
sudo apt-get install mysql-server
```

这将安装MySQL服务器的包，以及客户端和数据库公共文件的包。

在安装过程中，系统会要求您为root用户提供MySQL安装的密码。

## 离线安装_二进制手动安装

在下面的示例中，我们在`/usr/local/mysql` 目录中安装MySQL 5.7.24

> 警告

如果您以前使用操作系统本机程序包管理系统（如Yum或APT）安装了MySQL，则使用本机二进制文件进行安装时可能会遇到问题。确保您之前的MySQL安装已完全删除（使用您的包管理系统），并且还删除了任何其他文件，例如旧版本的数据文件。您也应该检查配置文件，如 `/etc/my.cnf`或 `/etc/mysql`目录，并删除它们。

### 安装依赖包

MySQL依赖于libaio libnuma库。如果未在本地安装此库，则数据目录初始化和后续服务器启动步骤将失败

```bash
// RedHat
yum install libaio libnuma
// Ubuntu
apt-get install libaio libnuma
```



### 下载二进制文件

*   [二进制文件](https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.24-linux-glibc2.12-x86_64.tar)

```bash
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.24-linux-glibc2.12-x86_64.tar
```

### MySQL安装布局

| 目录 | 目录的内容 |
| ---- | ---------- |
|`bin`|[**mysqld**](https://dev.mysql.com/doc/refman/5.7/en/mysqld.html "4.3.1 mysqld  -  MySQL服务器")服务器，客户端和实用程序|
|`docs`|信息格式的MySQL手册|
|`man`|Unix手册页|
|`include`|包含（标题）文件|
|`lib`|图书馆|
|`share`|用于数据库安装的错误消息，字典和SQL|
|`support-files`|其他支持文件|

### 创建一个mysql用户和组

添加`mysql`组和 `mysql`用户。

```bash
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
```

### 解压缩二进制安装包

```bash
cd /usr/local
tar zxvf mysql-5.7.24-linux-glibc2.12-x86_64.tar
```

接下来，创建一个指向**tar**创建的安装目录的符号链接：

```bash
ln -s  mysql-5.7.24-linux-glibc2.12-x86_64 mysql
```

该`ln`命令创建指向安装目录的符号链接。这使您可以更轻松地引用它`/usr/local/mysql`。为了避免在使用MySQL时必须始终键入客户端程序的路径名，

### 确保二进制文件位于`PATH`环境变量中列出的目录中。

修改$ PATH，以便可以调用[mysql](https://mariadb.com/kb/en/mysql-client/)，[mysqldump](https://mariadb.com/kb/en/mysqldump/)等客户端。

修改`.bashrc`或`.bash_profile`以使其永久化。

```bash
export PATH=$PATH:/usr/local/mysql/bin/
```


# 配置步骤

## 在线源YUM安装的启动方式

如果是通过在线源YUM安装，则无需配置直接启动数据库

```bash
// 启动服务
systemctl start mysqld
// 停止服务
systemctl stop mysqld
// 重启服务
systemctl restart mysqld
```

初始化安装时，将创建一个超级用户帐户'root'@'localhost，该超级用户的密码存储在错误日志文件中。要显示它，请使用以下命令：

```bash
sudo grep 'temporary password' /var/log/mysqld.log
```

通过使用生成的临时密码登录并为超级用户帐户设置自定义密码，尽快更改root密码：

```bash
mysql -uroot -p  -e "ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';"
```



*   注意

    [validate_password](https://dev.mysql.com/doc/refman/5.7/en/validate-password.html) 默认安装。实现的默认密码策略validate_password要求密码包含至少一个大写字母，一个小写字母，一个数字和一个特殊字符，并且密码总长度至少为8个字符。


## 在线源DEB安装的启动方式

MySQL服务器在安装后自动启动。您可以使用以下命令检查MySQL服务器的状态：

```bash
sudo service mysql status
```


使用以下命令停止MySQL服务器：

```bash
sudo service mysql stop
```

要重新启动MySQL服务器，请使用以下命令：

```bash
sudo service mysql restart
```

## 二进制包安装的启动方式

### 自动启动mysqld

您可以通过将文件`mysql.server`文件复制到正确的位置来使mysqld（MariaDB服务器）自动启动。

```bash
cp support-files/mysql.server /etc/init.d/mysql.server
systemctl start mysql
```

### 安装后

在此之后，请记住为可从不受信任的来源访问的所有帐户设置正确的密码，以避免让主机面临安全风险！

# 验证

执行到这一步能够成功将服务启动，通过mysql客户端工具访问本地的MariaDB服务即可。

查看后台进程是否启动

```bash
 ps -ef|grer mysql
```

查看监听端口是否启动 `ss -luntp | grep mysql`

客户端登陆方式：`mysql`
