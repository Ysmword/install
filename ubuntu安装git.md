1. 跳转到下载页面：https://git-scm.com/download/linux
2. 根据页面相关信息下载最新版本。关于Ubuntu信息如下：

Debian/Ubuntu
For the latest stable version for your release of Debian/Ubuntu
```sh
apt-get install git
```
For Ubuntu, this PPA provides the latest stable upstream Git version
```sh
add-apt-repository ppa:git-core/ppa # apt update; apt install git
```

3. 添加配置
```sh
git config --global user.name "username"
git config --global user.email "email"

# 查看是否配置成功
git config -l
```
