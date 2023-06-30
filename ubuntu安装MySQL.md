# Ubuntu安装MySQL
## 一. 首先卸载掉原来的mysql
第1步，依次执行下面的语句
```sh
su - root
apt-get autoremove --purge mysql-server
apt-get remove mysql-server
apt-get autoremove mysql-server
apt-get remove mysql-common 
```

第2步 清理残留数据
```sh
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```

第3步 验证原有主机上是否安装mysql
```sh
su - root
netstat -tap | grep mysql  # 命令查看是否有Mysql的端
```

## 二、安装msql
```sh
su - root
apt-get install mysql-server mysql-client
```

## 三、修改密码
```sh
su - root
vim /etc/mysql/debian.cnf
[client]
user = xxxx  # 修改值
passwork = xxxx # 修改值
```

## 四、登录验证
```sh
mysql -uxxxx -p
xxxx
```

## 五、运维方式
```sh
su - root
# 重启
service mysql restart

# 启动
service mysql start

# 停止
service mysql stop
```

# 卸载
我们以卸载mySQL5.7为例；

首先我们需要查看mysql依赖项，输入如下代码：
```sh
dpkg --list | grep mysql
```
以上代码输入后回车，会输出类似于如下的代码：
```sh
ii libmysqlclient-dev 5.7.34-0ubuntu0.18.04.1 amd64 MySQL database development files
ii libmysqlclient20:amd64 5.7.34-0ubuntu0.18.04.1 amd64 MySQL database client library
ii mysql-client-5.7 5.7.34-0ubuntu0.18.04.1 amd64 MySQL database client binaries
ii mysql-client-core-5.7 5.7.34-0ubuntu0.18.04.1 amd64 MySQL database core client binaries
ii mysql-common 5.8+1.0.4 all MySQL database common files, e.g. /etc/mysql/my.cnf
ii mysql-server-5.7 5.7.34-0ubuntu0.18.04.1 amd64 MySQL database server binaries and system database setup
ii mysql-server-core-5.7 5.7.34-0ubuntu0.18.04.1 amd64 MySQL database server binaries
```
然后我们就来卸载mysql-common，输入如下代码：
```
sudo apt remove mysql-common
```
接下来我们就可以卸载并清除mysql5.7，输入如下代码：
```
sudo apt autoremove --purge mysql-server-5.7
```

接下来我们就要来清除残留数据，输入如下代码：
```
dpkg -l | grep ^rc| awk '{print$2}'| sudo xargs dpkg -P
```

接下来我们在此检查依赖项，输入如下代码：
```
dpkg --list | grep mysql
```
如果输出为空，那么表示mysql已经彻底卸载干净了，如果不为空那么我们还要继续进行删除卸载，继续输入如下代码：
```
 sudo apt autoremove --purge mysql-apt-config
```
到底为止，Ubuntu上的mysql就已经彻底删除卸载干净了。


