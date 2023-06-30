1. 下载MySQL docker镜像，运行mysql
```sh
docker pull mysql/mysql-server:latest
```
执行docker run命令，运行mysql
```sh
docker run --name sc-mysql -v /data/mysql-8.0:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql/mysql-server:latest
```
2. 查看MySQL镜像运行状态
```sh
docker ps -a | grep mysql
```
3. 用容器id进入MySQL容器，执行mysql命令登录MySQL
```sh
docker exec -it d498d9f00612 /bin/bash

mysql -uroot -p123456
```

4. 查看用户信息
```sh
select  host, user, authentication_string, plugin from mysql.user;
```

5. 修改 root 用户 ，把host修改为%
```sh
use mysql;

update user set host = '%' where user = 'root';

FLUSH PRIVILEGES;

alter user 'root'@'%' identified with mysql_native_password by '123456';
```




