##### 13. while循环控制与语句嵌套
**`while_demo01.sh：`**
```shell
#!/usr/bin/bash
#Description：当i的值为5的时候，停止本循环
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/21 12:53

i=1
while [ $i -lt 10 ];do
    echo $i
    if [ $i -eq 5 ];then
        break
    fi
    i=$((i+1))
done
```
**`执行过程：`**
```shell
thanlon@thanlon-master:~$ bash while_demo01.sh 
1
2
3
4
5
```
**`while_demo01.sh：`**
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/21 13:03

i=0
while [ $i -lt 10 ];do
        i=$((i+1))
        if [ $i -eq 5 ];then
            continue
        fi
        echo $i
done
```
**`执行过程：`**
```shell
thanlon@thanlon-master:~$ bash while_demo02.sh 
1
2
3
4
6
7
8
9
10
```
>**`如果代码暂时不用了，可以把把它放到函数中！`**

相关案例：

**`九九乘法表的实现：`**
```shell
#!/usr/bin/bash
#Description：while实现九九乘法表
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/21 14:19
i=1
while [ $i -lt 10 ];do
        j=1
        while [ $j -lt $((i+1)) ];do
            echo -n "$j*$i=$((i*j)) "
            j=$((j+1))
        done
    i=$((i+1))
    echo
done
```
```shell
#!/usr/bin/bash
#Description：使用for实现九九乘法表
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/21 14:19
for((i=1;i<10;i++));do
    for((j=1;j<i+1;j++));do
            echo -n "$j*$i=$((i*j)) "    
    done
    echo
done
```
**`执行过程`**
```shell
1*1=1 
1*2=2 2*2=4 
1*3=3 2*3=6 3*3=9 
1*4=4 2*4=8 3*4=12 4*4=16 
1*5=5 2*5=10 3*5=15 4*5=20 5*5=25 
1*6=6 2*6=12 3*6=18 4*6=24 5*6=30 6*6=36 
1*7=7 2*7=14 3*7=21 4*7=28 5*7=35 6*7=42 7*7=49 
1*8=8 2*8=16 3*8=24 4*8=32 5*8=40 6*8=48 7*8=56 8*8=64 
1*9=9 2*9=18 3*9=27 4*9=36 5*9=45 6*9=54 7*9=63 8*9=72 9*9=81
```
**`使用while遍历文件内容：`**
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/21 18:47

while read i #读取$1文件，一行一行地赋值给i
    do
        echo "$i" #一行一行地输出
done < $1
```
**`执行过程：`**
```shell
thanlon@thanlon-master:~$ bash while_file.sh /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
……
```
**`使用while遍历文件内容，打印列：`**
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/21 18:57

#IFS指定默认的列分隔符
IFS=$":"
while read f1 f2 f3 f4
    do
        echo "$f1 $f2 $f3"
done < /etc/passwd
```
**`执行过程：`**
```shell
thanlon@thanlon-master:~$ bash while_file2.sh
root x 0
daemon x 1
bin x 2
sys x 3
sync x 4
games x 5
……
```
>**`注意：IFS指定默认的列分隔符`**