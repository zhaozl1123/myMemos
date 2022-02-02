# Confluence安装

## 1. 安装JAVA
```bash
# 安装java
yum -y install java-1.8*
# 测试java安装
java -version
```
![img](https://images2017.cnblogs.com/blog/1195249/201801/1195249-20180117135827303-599037240.png)

***

## 2. 安装mariadb-server数据库
```bash
yum install mariadb-server -y
systemctl start mariadb
systemctl enable mariadb
```
***

## 3. 配置MariaDB
### 1. 安装完成后首先要把MariaDB服务开启，并设置为开机启动
```bash
systemctl start mariadb  # 开启服务
systemctl enable mariadb  # 设置为开机自启动服务
```
### 2. 首次安装需要进行数据库的配置，命令都和mysql的一样
```bash
mysql_secure_installation
```
### 3. 配置时出现的各个选项
```bash
Enter current password for root (enter for none):  # 输入数据库超级管理员root的密码(注意不是系统root的密码)，第一次进入还没有设置密码则直接回车
Set root password? [Y/n]  # 设置密码，y
New password:  # 新密码
Re-enter new password:  # 再次输入密码
Remove anonymous users? [Y/n]  # 移除匿名用户， y
Disallow root login remotely? [Y/n]  # 拒绝root远程登录，n，不管y/n，都会拒绝root远程登录
Remove test database and access to it? [Y/n]  # 删除test数据库，y：删除。n：不删除，数据库中会有一个test数据库，一般不需要
Reload privilege tables now? [Y/n]  # 重新加载权限表，y。或者重启服务也许
```
### 4. 测试是否能够登录成功，出现 MariaDB [(none)]> 就表示已经能够正常登录使用MariaDB数据库了
```bash
mysql -u root -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 8
Server version: 5.5.60-MariaDB MariaDB Server
Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
MariaDB [(none)]>
```
### 5. 设置MariaDB字符集为utf-8
```bash
# /etc/my.cnf 文件
# 在 [mysqld] 标签下添加
init_connect='SET collation_connection = utf8_unicode_ci'
init_connect='SET NAMES utf8'
character-set-server=utf8
collation-server=utf8_unicode_ci
skip-character-set-client-handshake
# /etc/my.cnf.d/client.cnf 文件
# 在 [client] 标签下添加
default-character-set=utf8
# /etc/my.cnf.d/mysql-clients.cnf 文件
# 在 [mysql] 标签下添加
default-character-set=utf8
```
### 6. 重启服务
```bash
systemctl restart mariadb
```
### 7. 进入mariadb查看字符集
```bash
MariaDB [(none)]> show variables like "%character%";show variables like "%collation%";
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | latin1                     |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | latin1                     |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.01 sec)
    
+----------------------+-------------------+
| Variable_name        | Value             |
+----------------------+-------------------+
| collation_connection | utf8_general_ci   |
| collation_database   | latin1_swedish_ci |
| collation_server     | latin1_swedish_ci |
+----------------------+-------------------+
3 rows in set (0.00 sec)

+----------------------+-----------------+
| Variable_name        | Value           |
+----------------------+-----------------+
| collation_connection | utf8_unicode_ci |
| collation_database   | utf8_unicode_ci |
| collation_server     | utf8_unicode_ci |
+----------------------+-----------------+
3 rows in set (0.00 sec)

MariaDB [(none)]>
```
### 8. 远程链接mariadb数据库
```bash
# mariadb默认是拒绝 root 远程登录的。这里用的是 navicat 软件连接数据库
# 在不关闭防火墙的情况下，允许某端口的外来链接。步骤如下，开启3306端口，重启防火墙
[root@mini ~]# firewall-cmd --query-port=3306/tcp  # 查看3306端口是否开启
no
[root@mini ~]# firewall-cmd --zone=public --add-port=3306/tcp --permanent  # 开启3306端口
success
[root@mini ~]# firewall-cmd --reload  # 重启防火墙
success
[root@mini ~]# firewall-cmd --query-port=3306/tcp  # 查看3306端口是否开启
yes
```
### 9. 数据库配置
```bash
# 先查看mysql数据库中的user表
[root@mini ~]# mysql -u root -p  # 先通过本地链接进入数据库
MariaDB [(none)]> use mysql;
MariaDB [mysql]> select host, user from user;
+-----------+------+
| host      | user |
+-----------+------+
| 127.0.0.1 | root |
| ::1       | root |
| git.gitlab.cc| root |
+-----------+------+
3 rows in set (0.00 sec)
# 将与主机名相等的字段改为 "%" ，我的主机名为::1，
MariaDB [mysql]> update user set host='%' where host='::1';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [mysql]> select host, user from user;
+-----------+------+
| host      | user |
+-----------+------+
| %         | root |
| 127.0.0.1 | root |
| localhost | root |
+-----------+------+
3 rows in set (0.00 sec)
# 刷新权限表，或重启mariadb服务，一下二选一即可
MariaDB [mysql]> flush privileges;
Query OK, 0 rows affected (0.00 sec)
# 或者
[root@mini ~]# systemctl restart mariadb
# 重新远程链接mariadb，在宿主机使用Navicat
# 省略过程
```

## 4. 安装Confluence
```bash
# 下载软件tar.gz
# 下载confluence软件https://www.atlassian.com/software/confluence/download-archives
# 下载破解工具https://files.cnblogs.com/files/Javame/confluence破解工具.zip
# 下载mysql驱动https://files.cnblogs.com/files/Javame/confluence破解工具.rar

# 安装
# 复制jar至/opt/
tar -zxvf ....gz
# 在/opt/atlassian-confluence-5.10.4/confluence/WEB-INF/classes中，修改配置文件
vim confluence-init.properties  # 添加内容 confluence.home=/opt/data/conf/confluence
# 更名atlassian-confluence-5.10.4为atlassian-confluence
# /opt/atlassian-confluence/bin中启动./startup.sh
# 默认地址8090
# 选择生产性安装-...-记录ID-
# 复制/opt/atlassian-confluence/confluence/WEB-INF/lib目录下文件atlassian-extras-decoder-v2-3.2.jar，并重命名为atlassian-extras-decoder-2.4.jar
#windows中使用 java -jar ....jar，使用patch打包atlassian-extras-decoder-2.4.jar（重命名后），使用gen生成串号
# atlassian-extras-decoder-2.4.jar再次重命名为原名，放入/WEB-INF/lib中，同时放入mysql-connector-java-5.1.44-bin.jar
# 重新启动confluence ./startup.sh
# 输入串号
# 选择数据库-external Database-Direct JDBC
# 注意修改JDBC中数据库名称
# 在此之前，应当create confluenceDB
# 在mysql中
create database ConfluenceDB default character set utf8 collate utf8_bin;
grant all privileges on ConfluenceDB.* to 'root'@'%' identified by '0000';
flush privileges;

# 汉化
# Confluence-5.10.0-rc1-language-pack-zh_CN放入/WEB-INF/lib中，并在页面上add-on进行插件配置

# 设置开机自启动
# 修改开机启动文件：/etc/rc.local（或者/etc/rc.d/rc.local）
# 编辑rc.local文件
[root@localhost ~]# vi /etc/rc.local 
# 修改rc.local文件，在 exit 0 前面加入以下命令。保存并退出。/etc/init.d/mysqld start 
# mysql开机启动/etc/init.d/nginx start # nginx开机启动
supervisord -c /etc/supervisor/supervisord.conf
# supervisord开机启动/bin/bash /server/scripts/test.sh >/dev/null 2>/dev/null
# 最后修改rc.local文件的执行权限
[root@localhost ~]# chmod +x /etc/rc.local
[root@localhost ~]# chmod 755 /etc/rc.local

# 中文乱码
# 复制windows/Fonts内的字体至新建文件夹WinFonts
cp WinFonts至/usr/share/fonts/
vim /opt/atlassian-confluence/bin/setenv.sh  # 注意备份
# export前追加
CATALINA_OPTS="-Dconfluence.document.conversion.fontpath=/usr/share/fonts/WinFonts/ ${CATALINA_OPTS}"
# 清空confluence的home下viewfile目录和shared-home/dcl-document目录里的所有缓存文档文件
```

