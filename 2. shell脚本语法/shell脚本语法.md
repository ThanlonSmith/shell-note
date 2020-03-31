##### 2. shell脚本语法
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**`shell脚本就是将完成一个任务所有的命令按照执行的前后顺序，自上而下写入到一个文本文件中，然后给予执行权限。`**
###### 2.1 如何写shell脚本
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shell脚本的命名。要见名知意，如nginx的安装，可以写作“nginx_install”。名字不要太长，最好控制在30个字节以内。虽然Linux系统中没有扩展名的概念，但建议还是使用.sh来结尾。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shell脚本的格式。**`shell脚本的开头必须指定脚本的运行环境`**，以<kbd>**`#!`**</kbd>这个特殊符号组合完成。如#!/bin/bash指定该脚本运行解析由/usr/bin/bash来完成。解释环境的另外一种写法是：#!/usr/bin/env bash | python | perl。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shell脚本注释的使用。shell脚本中使用<kbd>**`#`**</kbd>号来注释文本，注意<kbd>**`#!`**</kbd>是特例，是专门用来指定脚本的运行环境。一般要带上脚本信息如：
```shell
# Author：Nai He
# Created Time：2020/03/29 20:00
# Release：1.0
# Script Description：nginx install script
```
###### 2.2 shell脚本运行方法
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shell脚本的运行方法有两种，一种是给执行权限运行，另一种是解释器直接运行(不需要给执行权限)。第一种：给脚本一个可执行权限后，找到该脚本的位置运行。第二种：可以使用bash解释器直接执行shell脚本，如`bash nginx_install.sh`。也可以使用sh解释器来执行shell，如`sh nginx_install.sh`，当然还可以使用其它解释器。查看系统中支持的shell解释器：
```python
thanlon@thanlon-master:~$ cat /etc/shells 
# /etc/shells: valid login shells
/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/bin/dash
/usr/bin/dash
```

###### 2.3 shell特殊符号
| ~      | !                                   | $            | + - * \ %                  | &        | *                         | ?            | ;                                             | \|                                           | \        | ``                     | '                                            | "                                                    |
| ------ | ----------------------------------- | ------------ | -------------------------- | -------- | ------------------------- | ------------ | --------------------------------------------- | -------------------------------------------- | -------- | ---------------------- | -------------------------------------------- | ---------------------------------------------------- |
| 家目录 | !表示执行历史命令，!!执行上一条命令 | 变量中取内容 | 对应数学运算，加减乘除取余 | 后台执行 | shell中的通配符，匹配所有 | 匹配一个字符 | 在shell中一行执行多条命令，命令之间用分好分隔 | 管道符，上一个命令的输出作为下一个命令的输入 | 转义字符 | 反引号，命令中执行命令 | 脚本中字符串用单引号引起来，单引号不解释变量 | 脚本中出现字符串可以使用双引号引起来，双引号解释变量 |
###### 2.4 shell管道的应用
管道在shell中使用最多，很多组合命令都需要使用管道来完成输出。管道符其实就是下一个命令对上一个命令的输出做处理。
###### 2.5 shell重定向
| >                      | >>                               | <          | <<             |
| ---------------------- | -------------------------------- | ---------- | -------------- |
| 重定向输入，覆盖原数据 | 重定向追加输入，在原数据末尾添加 | 重定向输出 | 重定向追加输出 |
值得注意的是重定向输入内容到同一个文件会先将原文件清空再写入，重定向输入和追加输入都比较常见，也很理解，主要重定向输出。

`重定向输出：`
```js
# 重定向输出，统计数据流和统计文本
thanlon@thanlon-master:~$ wc < naihe.txt 
 5  5 10
 thanlon@thanlon-master:~$ wc naihe.txt 
 5  5 24 naihe.txt
```
`重定向追加输出：`
```bash
#!/usr/bin/bash
#Author：Nai He
#Created Time：2020/03/31 08:30
#Script Description：harddisk partition script
fdisk /dev/sdb <<EOF
n
p
3

+100M
w
EOF
```
>**`问题：有四块硬盘 a、b、c、d，现要求每块硬盘分两个区，每个分区磁盘空间占硬盘空间的1/2，并且一个分区做成LVM-LVM100分区，挂载/data/lv100，另一个分区做成raid5分区，挂载/data/raid5，要求开机挂载。`**
###### 2.6 shell数学运算
expr命令只能做整数运算，注意空格：
```py
# 加法
thanlon@thanlon-master:~$ expr 10 + 10
20
# 减法
thanlon@thanlon-master:~$ expr 10 - 10
0
# 乘法
thanlon@thanlon-master:~$ expr 10 \* 10
100
# 除法
thanlon@thanlon-master:~$ expr 10 / 10
1
# $?是返回上一条命令是否执行成功的判断，0表示执行成功，非0表示上一条命令没有执行成功
thanlon@thanlon-master:~$ expr 10 % 10.0
expr: 非整数参数
thanlon@thanlon-master:~$ echo $?
2
thanlon@thanlon-master:~$ expr 10 % 10
0
thanlon@thanlon-master:~$ echo $?
1
thanlon@thanlon-master:~$ expr 10 % 4
2
thanlon@thanlon-master:~$ echo $?
0
# null是系统的回收站，黑洞
# 把命令expr 8 + 8执行的结果输出到/dev/null，用echo $?查看执行成功与否
thanlon@thanlon-master:~$ expr 8 + 8 &>/dev/null;echo $?
0
thanlon@thanlon-master:~$ expr 8 + 8.0 &>/dev/null;echo $?
2
```
使用let做计算，也是整数级的运算，注意不要使用空格：
```py
# 加
thanlon@thanlon-master:~$ let sum=10+10
thanlon@thanlon-master:~$ echo $sum 
20
# 减
thanlon@thanlon-master:~$ let a=10-5
thanlon@thanlon-master:~$ echo $a
5
# 乘
thanlon@thanlon-master:~$ let a=10*5
thanlon@thanlon-master:~$ echo $a
50
# 除
thanlon@thanlon-master:~$ let a=10/5
thanlon@thanlon-master:~$ echo $a
2
# 取余
thanlon@thanlon-master:~$ let a=10%5
thanlon@thanlon-master:~$ echo $a
0
```
使用bc计算器处理浮点运算，没有该模块可以使用`yum install bc`来安装：
```py
# 加法
thanlon@thanlon-master:~$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
10+10
20
10 +10
20
10 + 10
20
# 减法
thanlon@thanlon-master:~$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
20-10
10
20-10.3
9.7
# 乘法
thanlon@thanlon-master:~$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
10*1.0
10.0
# 除法
thanlon@thanlon-master:~$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
32/20.1
1
# 取余
thanlon@thanlon-master:~$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
19%29
19
19%29.8
19.0
# 混合运算
thanlon@thanlon-master:~$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
100*100/100
100
100*(2+3)/10
50
# 支持小数，保留指定位数的小数
thanlon@thanlon-master:~$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
scale=2
100/3
33.33
```
以上都是在交互，**`shell是不可以交互的`**，我们可以举个计算内存使用率的例子，把计算融入到shell中：
```py
# 查看内存空间相关
thanlon@thanlon-master:~$ free -mh
              总计         已用        空闲      共享    缓冲/缓存    可用
内存：       7.6Gi       1.8Gi       2.7Gi       538Mi       3.1Gi       5.0Gi
交换：       477Mi          0B       477Mi
# 计算内存的使用率
thanlon@thanlon-master:~$ echo "`echo "scale=2;1.8/7.6*100"|bc`%"
23.00%
# 计算内存的使用率，内部的echo可以使用单引号
thanlon@thanlon-master:~$ echo "`echo 'scale=2;1.8/7.6*100'|bc`%"
23.00%
```
使用bc计算器处理浮点运算，scale=2 代表小数点保留两位：
```py
# 加
thanlon@thanlon-master:~$ echo 'scale=2;100+100'|bc
200
# 减
thanlon@thanlon-master:~$ echo 'scale=2;100-100'|bc
0
# 乘
thanlon@thanlon-master:~$ echo 'scale=2;100*100'|bc
10000
# 除
thanlon@thanlon-master:~$ echo 'scale=2;100/100'|bc
1.00
# 取余
thanlon@thanlon-master:~$ echo 'scale=2;100%100'|bc
0
```
双小圆括号运算，在shell中((　))也可以用来做数学运算，注意这种运算也是整数级的运算：
```py
thanlon@thanlon-master:~$ echo $((100+100))
200
thanlon@thanlon-master:~$ echo $((100-100))
0
thanlon@thanlon-master:~$ echo $((100*100))
10000
thanlon@thanlon-master:~$ echo $((100/100))
1
thanlon@thanlon-master:~$ echo $((100%100))
0
# 开方运算
thanlon@thanlon-master:~$ echo $((100**3))
1000000
```
###### 2.7 脚本退出
exit NUM 退出脚本，释放系统资源，NUM代表一个整数，代表返回值。注意：**`NUM不能太大，它有个范围值1~255`**。
```py
# 正常情况下，看上一步是否执行成功，得到结果是０表示成功如
thanlon@thanlon-master:~$ echo $((100+100))
200
thanlon@thanlon-master:~$ echo $?
0
# 当然也可以定义返回的内容，具体操作如下：新建shell文件
thanlon@thanlon-master:~$ vim exit_code.sh
# 在该shell文件中输入以下内容，注意NUM不能太大
#!/bin/bash
echo 'thanlon'
exit 66
# 执行这个shell脚本exit_code.sh，然后看成功的返回值
thanlon@thanlon-master:~$ sh exit_code.sh 
thanlon
thanlon@thanlon-master:~$ echo $?
66
```