#   应用的后台运行配置
####    Linux/Unix
Shell脚本

*   关闭(stop.sh)
```
#!/bin/bash
PID=$(ps -ef | grep yourApp.java | grep -V grep | awk '{ print $2 }')

if [ -z "$PID"]
then
    echo the app is already stopped! 
else
    echo kill $PID
    kill $PID
fi
```

*   启动(start.sh)
```
#!/bin/bash
nohup java -jar yourApp.jar --server.port=8888 &
```

*   混合(先关闭后启动,run.sh)
```
#!/bin/bash
echo stop the application
source stop.sh
echo start the application
source start.sh
```

####    系统服务
*   APP软链至 /etc/init.d/ 目录下
    *   `sudo ln -s tmp/yourApp.jar /etc/init.d/yourApp`
*   应用的启动,停止,重启
    *   `/etc/init.d/yourApp start|stop|restart`
