## mac安装redis

### 使用brew安装

```sh
brew install redis
```

#### redis启动

```sh
brew services start redis
# 或
redis-server
```

#### 交互模式

```sh
redis-cli -h 127.0.0.1 -p 6379
```

如果你的brew抽风，无法下载，找安装包安装

### 使用安装包安装

安装方式跟Linux上的安装无异

安装方式为：https://github.com/Ysmword/install/blob/main/linxu%E5%AE%89%E8%A3%85redis
