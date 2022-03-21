## mongodb远程数据库导出到本地数据库

### 使用导出命令，将远程数据库数据备份到本地

```sh
# 以mac中使用brew安装mongo为例

# 远程数据库连接需要密码
mongodump --host=IP:PORT -u 用户名 -p 密码 -d 数据库 -o 文件存在路径 --authenticationDatabase=admin(一般都是admin，视情况而定）
# --authenticationDatabase:保存用户账号和密码的数据库

# 远程数据库连接不需要密码
mongodump --host=IP:PORT -d 数据库 -o 文件存在路径
```

### 使用导入命令，将远程数据库中的数据导入到本地数据库

```sh
# 以mac中使用brew安装mongo为例

# 本地数据库登录需要密码
mongorestore -h IP --port 端口 -u 用户名 -p 密码 -d 数据库(可以是已经存在的) --drop 文件存在路径 --authenticationDatabase=admin
# --drop是先删除所有的数据，再恢复，不需要删除可不加;
# --authenticationDatabase:保存用户账号和密码的数据库

# 本地数据库登录不需要密码
mongorestore -h IP --port 端口 -d 数据库(可以是已经存在的)
```

