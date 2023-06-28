# Linux安装mongo
- 访问https://www.mongodb.com/try/download/community
- 进入页面之后，点击On-premises->MongoDB Community Server，然后看向右侧找到有Downloads的框框，里面有版本号的下载
  - 如果不知道自己Linux属于哪个版本的，那就使用uname -a查看自己的Linux的版本
  - 如果都没有则找到3.6.23版本的，找到Platform选择框中找到Linux(legay)
- 如果是chrome可以在下载内容中找到链接：https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.23.tgz
- 使用wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.23.tgz命令进行下载
- 下载之后，使用tar -vxf mongodb-linux-x86_64-3.6.23.tgz进行解压
- 解压完之后，想要运行是不行滴，还需要安装依赖环境: https://www.runoob.com/mongodb/mongodb-linux-install.html
- 安装完依赖环境之后，执行以下命令
```sh
假设下载目录在/home/ysm下
mv mongodb-linux-x86_64-3.6.23 mongodb
cd mongodb
mkdir data   # 用于存储数据
mkdir conf   # 用于存储数据库配置
mkdir log    # 用于存储数据库产生的日志
cd log
touch mongo.log
cd ..
cd conf
vim mongo.conf   # 手动添加数据库配置
dbpath=/home/ysm/mongodb/data # 设置存储数据目录
logpath=/home/ysm/mongodb/log/mongo.log #设置存储日志文件
logappend=true    # 表示日志是以追加的方式写入
fork=true   # 表示后台运行
port=8897  # 访问数据库的端口
bind_ip=0.0.0.0  # 允许所有的IP地址访问
```
- 配置完之后，运行mongodb的server
```sh
cd /home/ysm/mongodb/bin
./mongod -f ../conf/mongo.conf   (不开启权限管理）
./mongod -f ../conf/mongo.conf --auth (开启权限管理）
```
- 开启完之后，使用client进行管理
```sh
cd /home/ysm/mongodb/bin
./mongo --port 8897 (这个端口与上面端口一致）
```

############################################################################################################################
# 简单权限管理
- 首先开启数据库的时候无需开启权限管理，这样才能够添加权限管理
```sh
./mongod -f ../conf/mongo.conf
```
- 使用客户端访问
```sh
./mongo --port 8897
```
- 创建超级管理员
```sh
use admin  # 切换到admin数据库
db.createUserdb.createUser({user:"useradmin",pwd:"useradmin",roles:[{role:"readWriteAnyDatabase",db:"admin"},{role:"dbAdminAnyDatabase",db:"admin"},{role:"clusterAdmin",db:"admin"}]})
```
- 退出，且杀死mongo进程后在开启
```sh
ps aux | grep "mongo" | grep "grep"
kill -QUIT pid (pid是mongo的进程号)
./mongod -f ../conf/mongo.conf --auth (开启权限管理）
```
- 使用客户端访问
```sh
./mongo --port 8897
```
- 进入admin，进行权限认证
```sh
use admin
db.auth("useradmin","useradmin")
```
- 可以直接使用其他的数据库了
```sh
use test
show collections
```


############################################################################################################################
# 启动脚本
```sh
#!/bin/bash
MY_PATH=`readlink -f $0`
ROOT_PATH=`dirname ${MY_PATH}`
CONF_FIFE=${ROOT_PATH}/conf/mongo.conf
MONGOD=${ROOT_PATH}/bin/mongod
LOG_PATH=${ROOT_PATH}/log/error.log

usage()
{
	echo "Usage: $0 start|stop|restart|status"
	exit 2
}

is_alive()
{
	if ps aux | grep -w mongod | grep -v grep > /dev/null
	then
		mongo_id=`ps aux | grep -w mongod | grep -v grep | awk '{print $2}'`
		return 0
	else
		return 1
	fi
}

mongo_status()
{
	if is_alive; then
		echo "mongo is running"
		return 0
	else 
		echo "mongo not running"
		return 1
	fi
}

mongo_start()
{
	if is_alive; then
		echo "mongo is running"
		return 0
	fi
	if [ -f CONF_FIFE ];then
		echo "no config file"
		return 1
	fi
	if [ -f MONGOD ];then
		echo "no binary file"
		return 1
	fi
	echo "------start mongo-------"
	${MONGOD} -f ${CONF_FIFE} 0</dev/null &>${LOG_PATH}
	sleep 1
	mongo_status
}
		
mongo_stop()
{
	if ! is_alive; then
		echo "mongo not running"
		return 0
	fi
	kill -INT ${mongo_id} 1>/dev/null 2>&1
	sleep 1
	echo "stop mongo DONE!"
}

mongo_restart()
{
	if ! is_alive; then
		echo "mongo not running"
		return 0
	fi
	echo "----stop mongo---"
	mongo_stop
	mongo_start
}


if [[ $# -gt 2 ]] || [[ $# -lt 1 ]]; then usage; fi

cd ${ROOT_PATH}

case "$1" in
"start")
	mongo_start;;
"stop")
	mongo_stop;;
"status")
	mongo_status;;
"restart")
	mongo_restart;;
*)
	usage;;
esac

exit $?
```
