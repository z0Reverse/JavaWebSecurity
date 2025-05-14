# Mysql安装

qwerTYUI123!!!

在CentOS 7.9上安装MySQL 5.7时，如果遇到“No package mysql-server-5.7 available”的错误，通常是因为默认的YUM仓库中没有包含MySQL 5.7的包。您需要手动添加MySQL官方的YUM仓库。以下是具体步骤：
```
1. 下载并安装MySQL官方YUM仓库
	sudo wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm 
	sudo rpm -Uvh mysql57-community-release-el7-11.noarch.rpm

2. 安装MySQL Server
	sudo yum install mysql-community-server

3. 启动并启用MySQL服务
	sudo systemctl start mysqld 
	sudo systemctl enable mysqld`

4. 获取临时密码
	sudo grep 'temporary password' /var/log/mysqld.log

5. 登录MySQL并修改密码
	mysql -u root -p 
	ALTER USER 'root'@'localhost' IDENTIFIED BY 'qwerQWER123!!!';

6. 配置防火墙规则（可选）
如果您需要从远程访问MySQL，确保您的ECS实例的安全组规则允许外部访问MySQL默认端口3306。


```
# mysql创建一个数据库以及为这个数据库分配一个账号用于jdbc连接

mysql> CREATE DATABASE ofcms;
Query OK, 1 row affected (0.00 sec)

mysql> CREATE USER 'ofcms'@'%' IDENTIFIED BY 'GS4BS2fw4b8CcZ4n!!!';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON ofcms.* TO 'ofcms'@'%';
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;

# Problem


Install 3 Packages (+3 Dependent packages) Total size: 220 M Is this ok [y/d/N]: y Downloading packages: warning: /var/cache/yum/x86_64/7/mysql57-community/packages/mysql-community-libs-5.7.44-1.el7.x86_64.rpm: Header V4 RSA/SHA256 Signature, key ID 3a79bd29: NOKEY Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql The GPG keys listed for the "MySQL 5.7 Community Server" repository are already installed but they are not correct for this package. Check that the correct key URLs are configured for this repository. Failing package is: mysql-community-libs-5.7.44-1.el7.x86_64 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql


在安装 MySQL 5.7 时，如果遇到 GPG 密钥验证失败的问题（如 `NOKEY` 或 `GPG Keys are not correct`），通常是因为 YUM 仓库的 GPG 密钥未正确导入或已过期。以下是解决此问题的步骤：
## 重装
```
1重载密钥
	sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql

2. 清理 YUM 缓存
	1. sudo yum clean all

3. 再次尝试安装 MySQL
	1. sudo yum install mysql-community-server

```
## 临时禁用密钥
```
sudo yum install mysql-community-server --nogpgcheck
```
