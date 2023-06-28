首先下载该脚本：
```sh
$ curl -fsSL https://get.docker.com -o get-docker.sh
```
现在以root权限运行该脚本：
```
$ sudo sh get-docker.sh
Executing docker install script
...
```

等到脚本达到完成。你应该看到一条确认信息，显示Docker已经安装。

> 这样有个缺点：这个脚本是为了提供一个通用的解决方案。如果不直接修改脚本的源代码，你就无法定制它的功能。它也不是为执行Docker更新而设计的，因为它不会将依赖关系更新到最新版本。



docker不需要sodu

1、创建一个docker组
```
$ sudo groupadd docker
```
2、添加当前用户到docker组
```
$ sudo usermod -aG docker $USER
```
添加之后记得重启terminal
