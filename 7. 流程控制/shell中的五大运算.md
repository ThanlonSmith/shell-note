##### 7. shell流程控制
###### 7.1 shell中的五大运算
1）数学比较运算
```shell
-eq # 等于
-ge # 大于等于
-gt # 大于
-le # 小于等于
-lt # 小于
-le # 不等于
```
你可以使用<kbd>man test</kbd>命令查看：
```py
……
       INTEGER1 -eq INTEGER2
              INTEGER1 is equal to INTEGER2

       INTEGER1 -ge INTEGER2
              INTEGER1 is greater than or equal to INTEGER2

       INTEGER1 -gt INTEGER2
              INTEGER1 is greater than INTEGER2

       INTEGER1 -le INTEGER2
              INTEGER1 is less than or equal to INTEGER2

       INTEGER1 -lt INTEGER2
              INTEGER1 is less than INTEGER2

       INTEGER1 -ne INTEGER2
              INTEGER1 is not equal to INTEGER2
……
```
<kbd>test</kbd>命令结合数学比较运算的简单使用1：
```shell
# 如果上一条命令执行成功，返回真就是0，
# test命令只会做判断，不会打印结果，我们需要使用组合命令
thanlon@thanlon-master:~$ test 1 -eq 1;echo $?
0
thanlon@thanlon-master:~$ test 1 -ge 1;echo $?
0
thanlon@thanlon-master:~$ test 1 -le 1;echo $?
0
thanlon@thanlon-master:~$ test 1 -lt 1;echo $?
1
thanlon@thanlon-master:~$ test 1 -gt 1;echo $?
1
thanlon@thanlon-master:~$ test 1 -ne 1;echo $?
1
thanlon@thanlon-master:~$ echo "1.5*10"
1.5*10
thanlon@thanlon-master:~$ echo "1.5*10"|bc
15.0
thanlon@thanlon-master:~$ echo "1.5*10"|bc
15.0
# 15.0以小数点分割，取小数点前面的数，使用f1
thanlon@thanlon-master:~$ echo "1.5*10"|bc|cut -d '.' -f1
15
# 15.0以小数点分割，取小数点后的数，使用f2
thanlon@thanlon-master:~$ echo "1.5*10"|bc|cut -d '.' -f2
0
thanlon@thanlon-master:~$ test `echo "1.5*10"|bc|cut -d '.' -f2` -eq 20;echo $?
1
thanlon@thanlon-master:~$ test `echo "1.5*10"|bc|cut -d '.' -f2` -eq $((2*10));echo $?
1
```
<kbd>test</kbd>命令结合数学比较运算的简单使用2：

`float.sh：`
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/13 21:20
num01=`echo "1.5*10"|bc|cut -d "." -f1`
num02=$((2*10))

test $num01 -ge $num02;echo $?
```
`执行过程：`

```shell
thanlon@thanlon-master:~/工程/ShellProjects$ bash float.sh 
1
# -x是查看debug的过程
thanlon@thanlon-master:~/工程/ShellProjects$ bash -x float.sh 
++ echo '1.5*10'
++ bc
++ cut -d . -f1
+ num01=15
+ num02=20
+ test 15 -ge 20
+ echo 1
1
```
>**`注意：数学运算比较的是整型的数据!`**

