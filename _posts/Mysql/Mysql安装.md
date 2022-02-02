# Mysql安装

## 安装
```bash
# 下载安装包 mysql-5.6.40-linux-glibc2.12-x86_64.tar.gz
# 略
# 卸载系统自带的Mariadb
rpm -qa|grep mariadb      //查询已安装的mariadb
rpm -e --nodeps 文件名  //卸载,文件名为使用rpm -qa|grep mariadb 命令查出的所有文件
# 删除etc目录下的my.cnf文件（若有）
rm /etc/my.cnf
# 创建mysql用户组
groupadd mysql
# 创建一个用户名为mysql的用户并加入mysql用户组
useradd -g mysql mysql
# 将下载的二进制压缩包放到/usr/local/目录下
# 略
# 解压安装包
tar -zxvf mysql-5.6.40-linux-glibc2.12-x86_64.tar.gz
# 将解压好的文件夹重命名为mysql

mv mysql-5.6.40-linux-glibc2.12-x86_64.tar.gz mysql
# 在etc下新建配置文件my.cnf
> [mysql]
> # 设置mysql客户端默认字符集
> default-character-set=utf8
> socket=/var/lib/mysql/mysql.sock
> [mysqld]
> skip-name-resolve
> #设置3306端口
> port=3306
> socket=/var/lib/mysql/mysql.sock
> # 设置mysql的安装目录
> basedir=/usr/local/mysql
> # 设置mysql数据库的数据的存放目录
> datadir=/usr/local/mysql/data
> # 允许最大连接数
> max_connections=200
> # 服务端使用的字符集默认为8比特编码的latin1字符集
> character-set-server=utf8
> # 创建新表时将使用的默认存储引擎
> default-storage-engine=INNODB
> lower_case_table_names=1
> max_allowed_packet=16M
# 创建步骤9中用到的目录并将其用户设置为mysql
mkdir /var/lib/mysql
mkdir /var/lib/mysql/mysql
chown -R mysql:mysql /var/lib/mysql
chown -R mysql:mysql /var/lib/mysql/mysql
# 进入安装mysql软件目录
cd /usr/local/mysql
chown -R mysql:mysql ./　　              #修改当前目录拥有者为mysql用户
./bin/mysqld --initialize  # 数据库初始化
chown -R mysql:mysql data                   #修改当前data目录拥有者为mysql用户
```

## 配置
```bash
# 授予my.cnf的最大权限。
chown 777 /etc/my.cnf
# 设置开机自启动服务控制脚本：
# 复制启动脚本到资源目录
cp ./support-files/mysql.server /etc/rc.d/init.d/mysqld 
# 如果没有rc.d直接输入/etc/init.d/mysqld即可   
# 增加mysqld服务控制脚本执行权限
chmod +x /etc/rc.d/init.d/mysqld
# 将mysqld服务加入到系统服务
chkconfig --add mysqld
# 检查mysqld服务是否已经生效
chkconfig --list mysqld
# 命令输出类似下面的结果：
mysqld 0:off 1:off 2:on 3:on 4:on 5:on 6:off
# 表明mysqld服务已经生效，在2、3、4、5运行级别随系统启动而自动启动，以后可以使用service命令控制mysql的启动和停止。
# 启动msql（停止mysqld服务：service mysqld stop）
service mysqld start
# 将mysql的bin目录加入PATH环境变量，编辑/etc/profile文件
vi /etc/profile
# 在文件最后添加如下信息：
export PATH=$PATH:/usr/local/mysql/bin
# 执行下面的命令使所做的更改生效：
source /etc/profile
# 以root账户登陆mysql，默认是没有密码(直接回车)
mysql -u root -p
# 设置root账户密码 注意下面的you password改成你的要修改的密码
use mysql;
alter user 'root'@'localhost' identified with mysql_native_password by '000000';
# 设置远程主机登录，注意下面的your username 和 your password改成你需要设置的用户和密码
# 先通过本地链接进入数据库
[root@mini ~]# mysql -u root -p  
MariaDB [(none)]> use mysql;
MariaDB [mysql]> select host, user from user;
+-----------+------+
| host      | user |
+-----------+------+
| 127.0.0.1 | root |
| ::1       | root |
| git.gitlab.cc| root |
+-----------+------+
# 如果结果如上，使用下述命令修改远程权限
update user set host='%' where host='::1';
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
# 否则，使用下述命令新建远程连接用户
GRANT ALL PRIVILEGES ON *.* TO'your username'@'%' IDENTIFIED BY 'your password' WITH GRANT OPTION;
# 最终，更新权限
FLUSH PRIVILEGES ;
# 对于8.0以后的MySQL，使用如下命令
CREATE USER 'root'@'%' IDENTIFIED BY 'your password'; 
GRANT ALL ON *.* TO 'root'@'%'; 
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'your password';
FLUSH PRIVILEGES;

```

