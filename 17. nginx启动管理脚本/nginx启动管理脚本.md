##### 17. nginx启动管理脚本
请确保您的电脑已安装nginx，我这里将nginx安装在CentOS 7系统中。

**`nginxd.sh`**
```shell
#!/usr/bin/bash

#参数
#nginx的安装目录
nginx_install_doc=/usr/local/nginx1180 #实际上就是字符串
#nginx的启动命令
nginxd=$nginx_install_doc/sbin/nginx
#nginx存放PID的文件
pid_file=$nginx_install_doc/logs/nginx.pid
#自定义变量用来代替nginx
proc=nginx

#调用系统提供的函数库
. /etc/init.d/functions #.就是source
#判断有无函数库文件
if [ -f /etc/init.d/functions ];then
    . /etc/init.d/functions
else
    echo "not found file /etc/init.d/functions"
fi	
#if [ -f $pid_file ];then
    #nginx_process_id=`cat $pid_file` 
    #nginx_process_num=`ps aux|grep proc|grep -v "grep"|wc -l`
#fi
#获取nginx进程数
nginx_process_num=`ps aux|grep proc|grep -v "grep"|wc -l`

#启动nginx函数
start(){
if [ -f $pid_file ]&&[ $nginx_process_num -ge 1 ];then
    echo "nginx is running..."
else
    if [ -f $pid_file ]&&[ $nginx_process_num -lt 1 ];then
        rm -rf $pid_file #启动失败或断电等导致pid文件没有被删除,正常情况是nginx退出pid文件就被删除
        #echo "nginx started.`daemon $nginxd`" #启动nginx程序,daemon函数来自函数库
        action "nginx started." $nginxd
    fi
    #echo "nginx started`daemon $nginxd`"
    action "nginx started." $nginxd
fi
}

#停止nginx函数
stop(){
if [ -f $pid_file ]&&[ $nginx_process_num -ge 1 ];then
    action "nginx stoped" killall -s QUIT $proc
    rm -f $pid_file
else
    action "nginx stoped." killall -s QUIT $proc 2>/dev/null
fi
}

#重启nginx函数
restart(){
    stop
    sleep 1 # 确保上一步能完成
    start
}

#重载nginx
reload(){
if [ -f $pid_file ]&&[ $nginx_process_num -ge 1 ];then
    action "nginx reloaded." killall -s HUP $proc
else
    action "nginx reloaded." killall -s HUP $proc 2>/dev/null
fi
}

#nginx状态
status(){
if [ -f $pid_file ]&&[ $nginx_process_num -ge 1 ];then
    action "nginx running..."
else
    action "nginx stoped."
fi
}

case $1 in
start)start;;
stop)stop;;
restart)restart;;
reload)reload;;
status)status;;
*)echo "$USAGE:$0 start|stop|restart|reload|status";;
esac
```
`脚本执行步骤：`
```js
[root@test-14 ~]# ./nginxd.sh start
nginx started.                                             [  确定  ]
[root@test-14 ~]# ./nginxd.sh start
nginx is running...
[root@test-14 ~]# ./nginxd.sh stop
nginx stoped                                               [  确定  ]
[root@test-14 ~]# ./nginxd.sh stop
nginx stoped.                                              [失败]
[root@test-14 ~]# ./nginxd.sh start
nginx started.                                             [  确定  ]
[root@test-14 ~]# ./nginxd.sh restart
nginx stoped                                               [  确定  ]
nginx started.                                             [  确定  ]
[root@test-14 ~]# ./nginxd.sh reload
nginx reloaded.                                            [  确定  ]
[root@test-14 ~]# ./nginxd.sh status
nginx running...                                           [  确定  ]
[root@test-14 ~]# ./nginxd.sh stop
nginx stoped                                               [  确定  ]
[root@test-14 ~]# ./nginxd.sh status
nginx stoped.          
```
```shell
# 可以将脚本复制到/etc/init.d/下并命名为nginxd，让其可以被当作系统服务管理脚本用service命令执行
[root@test-14 ~]$ cp nginxd.sh /etc/init.d/nginxd
```
>**可以使用killall命令杀掉nginx，杀掉nginx之后pid文件就没有了。**