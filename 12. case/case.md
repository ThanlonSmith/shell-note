##### 12. case
###### 12.1 case介绍
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;case语句是多条件分之语句。在生产环境中，我们会遇到一个问题需要根据不同的情况来执行不同的预案，那么我们要处理这些问题就要首先根据可能出现的情况写出对应的预案，根据出现的情况来加载不同的预案。实际中也有这样的例子，**`如监控内存的使用率`**。
###### 12.2 case语法
```shell
case 变量 in
条件1)
			执行代码块1
;;
条件2)
			执行代码块2
;;
……
esac
```
>**`注意：每个代码块执行结束要以;;结尾代表结束。case结尾要以反转的esac来结束。`**

相关案例：
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/19 13:36

read -p "请输入您要查找的职工姓名：" N
case $N in
Thanlon)
    echo "1.姓名：Thanlon"
    echo "2.性别：男"
    echo "3.年龄：23"
;;
Kili)
    echo "1.姓名：Kili"
    echo "2.性别：女"
    echo "3.年龄：21"
;;
Kiku)
    echo "1.姓名：Kiku"
    echo "2.性别：女"
    echo "3.年龄：24" 
;;
esac
```
```shell
thanlon@thanlon-master:~/工程/ShellProjects$ bash case_demo.sh 
请输入您要查找的职工姓名：Thanlon
1.姓名：Thanlon
2.性别：男
3.年龄：23
thanlon@thanlon-master:~/工程/ShellProjects$ bash case_demo.sh 
请输入您要查找的职工姓名：Kili
1.姓名：Kili
2.性别：女
3.年龄：21
thanlon@thanlon-master:~/工程/ShellProjects$ bash case_demo.sh 
请输入您要查找的职工姓名：Kiku
1.姓名：Kiku
2.性别：女
3.年龄：24
```
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/19 14:02

case $1 in
nn|NN)
    echo "奶奶好！"
;;
lzr|LZR)
    echo "伯父好！"
;;
zmn|ZMN)
    echo "伯母好！"
;;
*)
    echo "USAGE：$0 nn|lzr|zmn"
;;
esac
```
```shell
thanlon@thanlon-master:~/工程/ShellProjects$ bash case_demo.sh
USAGE：case_demo.sh nn|lzr|zmn
thanlon@thanlon-master:~/工程/ShellProjects$ bash case_demo.sh nn
奶奶好！
thanlon@thanlon-master:~/工程/ShellProjects$ bash case_demo.sh lzr
伯父好！
thanlon@thanlon-master:~/工程/ShellProjects$ bash case_demo.sh zmn
伯母好！
```