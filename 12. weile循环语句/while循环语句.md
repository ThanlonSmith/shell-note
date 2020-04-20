##### 12. while循环语句
###### 12.1 while循环介绍
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;while 和 for一样都是 shell 中负责循环的语句。for是条件循环，是根据条件的个数来决定循环的个数。**`当我们明确知道循环次数，使用for。如果不知道循环多少次，使用while。 `**
###### 12.2 while循环语法
```shell
while [ condition ]
do
    代码块
done
```
###### 12.3 while循环案例
**`while_demo01.sh：`**
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/20 22:32

read -p "money：" money
read -p "car_num：" car_num
read -p "house_num" house_num
while [ $money -lt 100000 ]||[ $car -lt 1 ]||[ $house_num -lt 1 ]
    do
        echo "不满足条件！"
        read -p "money：" money
        read -p "car_num：" car_num
        read -p "house_num" house_num
done
echo "满足条件！"
```
**`执行过程：`**
```shell
thanlon@thanlon-master:~$ bash while_demo01.sh 
money：100000
car_num：1
house_num1
满足条件！
thanlon@thanlon-master:~$ bash while_demo01.sh 
money：100000
car_num：0
house_num1
不满足条件！
money：100000
car_num：1
house_num0
不满足条件！
money：100000
car_num：1
house_num1
满足条件！
thanlon@thanlon-master:~$ 
```
**`while_demo02.sh：`**
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/20 22:36

read -p "Account: " account
while [ $account != "root" ]
do
    read -p "Account: " account
done
```
**`执行过程：`**
```shell
thanlon@thanlon-master:~$ bash while_demo02.sh 
Account: thanlon
Account: kili
Account: root
```
**`while_demo03.sh：`**
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/20 22:48

while [ ! -d /tmp/thanlon/ ]
do
    echo "not found /tmp/thanlon/"
    sleep 2
done
```
**`执行过程：`**
```shell
控制台1：
# 控制台2中创建了目录后，脚本执行结束
thanlon@thanlon-master:~$ bash while_demo03.sh
not found /tmp/thanlon/
not found /tmp/thanlon/
not found /tmp/thanlon/
not found /tmp/thanlon/
thanlon@thanlon-master:~$ 

控制台2：

thanlon@thanlon-master:~$ mkdir /tmp/thanlon/
```