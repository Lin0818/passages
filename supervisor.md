
##### 参考网址：
官方网站：(http://supervisord.org/)

##### 安装方法：
```shell
sudo yum install python-pip  #安装python 安装脚本
sudo pip install supervisor  
sudo easy_install supervisor
```

##### 安装完成后，有三个程序
```shell
supervisord  #后台守护进程
supervisorctl  #控制程序
echo_supervisord_conf  #生成配置文件
```

##### 生成配置文件
```shell
echo_supervisord_conf > /etc/supervisord.conf
```

##### 启动supervisor服务
```
supervisord -c /etc/supervisord.conf
```

##### 配置文件重要点
如果服务器需要管理多个进程，可以使用include来管理多个conf文件，也可以追加到supervisord.conf文件后面，为了便于管理，最好使用include
```
[include]
files = /etc/supervisord/*.conf
```

示例 redis-console-nodejs 启动
```
[program:redis-console_node]
command=/usr/local/bin/node server/bin/www CONFIG=/export/Config/redis-console6.jcloud.com/index.js             ; the program (relative uses PATH, can take args)
autostart=true                ; start at supervisord start (default: true)
autorestart=unexpected        ; whether/when to restart (default: unexpected; false, true)
startsecs=1                   ; number of secs prog must stay running (def. 1)
startretries=1000000
user=root                   ; setuid to this UNIX account to run the program
stdout_logfile=/export/Logs/redis-console6.jcloud.com/access.log        ; stdout log path, NONE for none; default AUTO
stderr_logfile=/export/Logs/redis-console6.jcloud.com/error.log        ; stderr log path, NONE for none; default AUTO
directory=/export/App/redis-console6.jcloud.com/current
```


##### supervisorctl 命令详解
```
supervisorctl update  #重新加载supervisor的配置文件，不重启
supervisorctl reload #重新启动supervisor
supervisorctl status #查看子进程启动状态
#启动redis-console_node子进程
supervisorctl start redis-console_node
#重启redis-console_node子进程
supervisorctl restart redis-console_node
#停止redis-console_node子进程
supervisorctl stop redis-console_node

#进入supervisor交互模式
supervisorctl
> help #查看帮助
> quit #退出
```