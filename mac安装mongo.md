### 使用brew安装

```sh
brew tap mongodb/brew
brew install mongodb-community@4.4
# @符号后面的4.4是最新的版本号，如果想要看其他版本，可以执行brew search mongo查看
```

安装信息

- 安装mongo路径为：/opt/homebrew/Cellar/mongodb-community@4.4/4.4.13
- mongo的配置文件路径为：/opt/homebrew/etc/mongod.conf
- mongo的数据存放路径为：/opt/homebrew/var/mongodb

### 运行mongodb

#### 使用brew命令启动

brew启动

```sh
brew services start mongodb-community@4.4
```

brew停止

```sh
brew services stop mongodb-community@4.4
```

#### 使用mongod命令后台进程

```sh
cd /opt/homebrew/Cellar/mongodb-community@4.4/4.4.13/bin
./mongod --config /opt/homebrew/etc/mongod.conf --fork
```

这种方式启动，关闭的话可以进入mongo shell控制台来实现

```sh
cd /opt/homebrew/Cellar/mongodb-community@4.4/4.4.13/bin
./mongo
db.adminCommand({ "shutdown" : 1 })
```

如果上面的因为网络问题导致无法顺利的下载，可以执行方案B

## 方案B

将mac看成Linux，只不过在选择版本的时候注意点即可。

具体安装方法为：https://github.com/Ysmword/install/blob/main/linux%E5%AE%89%E8%A3%85mongo
