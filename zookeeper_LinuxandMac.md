# zookeeper安装(仅仅不适用于window环境）

- 安装jdk。安装教程为：https://www.centoscn.vip/5209.html

- 下载zookeeper:https://zookeeper.apache.org/releases.html

- 解压下载文件：tar -xzvf apache-zookeeper-3.6.3-bin.tar.gz

- 将文件放置：/usr/local目录下

  - ```
    mv /Users/yangshimiao/Downloads /usr/local/zookeeper
    ```

- 配置环境变量

  - ```sh
    vim /etc/profile
    # 添加如下内容
    # zookeeper
    export ZK_HOME=/usr/local/zookeeper/bin
    export PATH=$PATH:$ZK_HOME
    
    # 将profile编译
    source /etc/profile
    ```

- 启动zookeeper

  - zkServer.sh start

- 停止zookeeper

  - zkServer.sh stop



参考资料：

https://www.cnblogs.com/qingjiawen/p/14359062.html


# docker 安装 zookeeper
1. docker安装zookeeper
下载zookeeper 最新版镜像

```sh
docker search zookeeper    
docker pull zookeeper 
docker images              //查看下载的本地镜像
docker inspect zookeeper   //查看zookeeper详细信息
```

新建一个文件夹
mkdir zookeeper
挂载本地文件夹并启动服务

```sh
docker run -d -e TZ="Asia/Shanghai" -p 2181:2181 -v /root/docker/zookeeper:/data --name zookeeper --restart always zookeeper
```

参数解释
```sh
-e TZ="Asia/Shanghai" # 指定上海时区 
-d # 表示在一直在后台运行容器
-p 2181:2181 # 对端口进行映射，将本地2181端口映射到容器内部的2181端口
--name # 设置创建的容器名称
-v # 将本地目录(文件)挂载到容器指定目录；
--restart always #始终重新启动zookeeper
```

查看容器
```sh
docker ps
```
进入容器(zookeeper)

第一种方式
```sh
 docker run -it --rm --link zookeeper:zookeeper zookeeper zkCli.sh -server zookeeper       //这样的话，直接登录到容器时，进入到 zkCli中
```
第二种方式（推荐）
```sh
docker exec -it zookeeper bash      //只登录容器，不登录 zkCli
./bin/zkCli.sh    //执行脚本新建一个Client，即进入容器
```
