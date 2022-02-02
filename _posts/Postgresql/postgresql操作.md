# Postgresql操作

## 启动pgAdmin的Docker
```bash
docker run -it -p 80:80 -e 'PGADMIN_DEFAULT_EMAIL=admin@pgadmin.com' -e 'PGADMIN_DEFAULT_PASSWORD=admin' --name pgadmin dpage/pgadmin4
```

## 创建用户、创建数据库、授权数据库给用户
```bash
# 创建角色并设置密码
create user admin with password 'admin';
> CREATE ROLE
# 修改数据库用户和密码
postgres=# alter user admin with password '558996';
> ALTER ROLE
# 指定字符集创建数据库testdb1，并且授权给testwjw
postgres=# create database testdb1 with encoding='utf8' owner=testwjw;
> CREATE DATABASE
# 授权给testwjw
postgres=# grant all privileges on database testdb1 to testwjw; 
> GRANT
```
## 设置远程登陆
```bash
# 新增对外地址与端口
# 在postgresql.conf中，修改port:36985,修改监听地址listen_addresses = '*'
# 在pg_hba.conf中，修改host all all 172.17.0.2/32 trust
# 重启postgresql服务systemctl restart postgresql-13
```
