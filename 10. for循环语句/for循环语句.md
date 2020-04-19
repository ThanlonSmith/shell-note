##### 9. for 循环语句
###### 9.1 for 循环介绍
脚本在执行任务的时候，总是会遇到循环执行的时候，比如说我们需要脚本每隔一段时间执行一次ping操作。除了计划任务可以实现，还可以使用脚本来完成，需要用到循环语句。for循环叫做条件循环，for循环的次数和给予的条件是成正比的。
>**`在完成同一个任务时，使用循环可以节省内存；并且使用循环是程序结构更清晰；`**
###### 9.2 for 语法
1）语法一
```shell
for var in value1 value2 value3……
    do
        commands
done
```
循环输出1~9个数字：
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/19 22:10

for i in `seq 1 9` # 使用命令赋值
    do
        echo $i
done
```
```shell
thanlon@thanlon-master:~$ bash for_demo01.sh 
1
2
3
4
5
6
7
8
9
```
>**`seq 1 9 是命令赋值，for var in 1 2 3 4 是直接赋值。还可以赋予字符串，如 for var in thanlon\'s bag, kili\'s bag`**
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/19 22:18

for var in thanlon\'s is cool,
    do
        echo $var
done
```
```shell
thanlon@thanlon-master:~$ bash for_demo02.sh 
thanlon's
is
cool,
```
2）语法二
```shell
for ((变量;条件;自增减运算))
    do
        代码块
done 
```
循环输出1~9个数字：
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/19 22:10

# C格式语法
for((i=0;i<10;i++))
    do
        echo $i
done
```
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/19 22:18

# 多变量的C格式语法
for((a=0,b=9;a<10;a++,b--)) #a++=a+1,b--=b-1
    do
        echo $a $b
done
```
```shell
thanlon@thanlon-master:~$ bash for_demo02.sh 
0 9
1 8
2 7
3 6
4 5
5 4
6 3
7 2
8 1
9 0
```
>**`使用((;;))条件可以实现无限循环。`**

编写一个无线循环的脚本：
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/20 00:54

for((;;))
    do
        echo "Hello World!"
done
```