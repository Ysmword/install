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

## 六、设置远程链接
需要打开MySQL的配置文件my.cnf，这个文件通常位于/etc/mysql/目录下。在此文件中，我们需要将bind-address选项的值改为0.0.0.0：
```conf
bind-address = 0.0.0.0
```
然后重启下：service mysql restart


