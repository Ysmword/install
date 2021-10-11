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
