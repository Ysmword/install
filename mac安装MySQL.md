# mac安装MySQL

- 到社区下载安装包：https://dev.mysql.com/downloads/mysql/

  - 在mac的终端中使用uname -a的命令查看机器信息
  - 根据机器信息下载安装包
![image](https://user-images.githubusercontent.com/41908749/140790285-ea7ae9c6-9640-411b-b3e6-c73ae91e084a.png)

- 点击安装包，一路next即可

- 安装完毕之后，在系统偏好设置，找到有MySQL的图标，就表明安装成功

![image](https://user-images.githubusercontent.com/41908749/140790198-4706639b-0674-4fe2-a0f0-c4ea1075226a.png)

- 终端登录MySQL

  - 我们在终端输入`mysql`,发现提示`commod not found`，那是因为我们没配置系统的环境变量

    - 找到MySQL的可执行文件所处路径：/usr/local/mysql/bin
    - 如果是`bash`,执行`vim ~/.bash_profile`；如果是`zsh`,执行`vim ~/.zshrc`
    - 添加语句`PATH=$PATH:/usr/local/mysql/bin`,保存
    - 立即生效，`source ~/.bash_profile` or `source ~/.zshrc`
  - 使用命令登录MySQL
    - mysql -uroot -p
      - 如果忘记密码，可以在系统偏好设置中找到MySQL图标，点击进入管理界面，然后点击initialize Database进行初始化，最后在管理界面点击包含有start的按钮就可以了
