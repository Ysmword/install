1. 打开官网下载地址选择对应的系统版本：https://studygolang.com/dl
2. 在安装目录下运行以下命令，即将安装包下载到目录下：
```sh
 wget https://studygolang.com/dl/golang/go1.20.5.linux-amd64.tar.gz
```
3. 执行tar解压
```sh
tar -xf go1.20.5.linux-amd64.tar.gz
```
4. 将go的bin目录放置到PATH变量中。添加到/etc/profile
```sh
vim /etc/profile
export GOROOT=/home/work/software/golang/go
export PATH=$PATH:$GOROOT/bin
# 保存后source下
source /etc/profile
5. 执行go version 查看是否更新成功

