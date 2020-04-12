##### 6. shell数组
###### 6.1 数组介绍
变量只能存一个值，但是当需要存储很多个值的时候，定义很多个变量是不可行的，所以引出了数组。数组和变量都可以存数据，不同之处在于数组可以存多个值，而变量只能存一个值。
###### 6.2 基本数组
数组可以让用户一次赋予多个值，需要读取数据时只需要通过索引调用就可以方便读出来。

1）数组语法
```shell
数组名称 = (元素1, 元素2, 元素3,...)
```
2）数组的读取
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/12 10:51
arr01=('thanlon' 'kiku' 'kili')
echo ${arr01[0]}
echo ${arr01[1]}
echo ${arr01[2]}
```
>**同大多数编程语言中的数组一样，数组的索引是从0开始的。**

3）数组赋值

① 一次赋一个值
```shell
array[0]='thanlon'
array[1]='kiku'
array[2]='kili'
```
② 一次赋多个值
```shell
array01=(thanlon kiku kili)
array02=(`cat /etc/passwd`)
array03=(`ls /var/ftp/Shell/for*`)
array04=(thanlon kiku kili "bash shell")
```
4）数组的查看
```shell
# 查看系统中声明过的数组
thanlon@thanlon-master:~$ declare -a
declare -a BASH_ARGC=([0]="0")
declare -a BASH_ARGV=()
declare -a BASH_COMPLETION_VERSINFO=([0]="2" [1]="9")
declare -a BASH_LINENO=()
declare -ar BASH_REMATCH=()
declare -a BASH_SOURCE=()
declare -ar BASH_VERSINFO=([0]="5" [1]="0" [2]="3" [3]="1" [4]="release" [5]="x86_64-pc-linux-gnu")
declare -a DIRSTACK=()
declare -a FUNCNAME
declare -a GROUPS=()
declare -a PIPESTATUS=([0]="0")
```
5）访问数组元素
```shell
# 查看自定义的数组
echo ${array[0]} # 访问数组中的第一个元素
echo ${array[@]} # 访问数组中的所有元素
echo ${#array[@]} # 统计数组中元素的个数
echo ${!array[@]} # 获取数组元素的索引
echo ${array[@]:1} # 从数组下标1开始
echo ${array[@]:1:2} # 从数组下标1开始访问两个元素
```
6）遍历数组
```shell
# 默认通过数组元素的个数进行遍历
echo ${arr01[0]}
echo ${arr01[1]}
echo ${arr01[2]}
```
>**针对关联数组可以通过数组元素的索引值进行遍历。**
###### 6.3 关联数组
关联数组可以允许用户自定义数组的索引，这样使用起来会更加方便。

1）定义关联数组
```shell
# 申明关联数组变量
thanlon@thanlon-master:~$ declare -A ass_array01
```
>**关联数组用大“A”参数申明，索引数组使用小“a”参数申明。**

2）关联数组赋值

一次赋一个值：
```shell
# 数组名[索引]=变量名
thanlon@thanlon-master:~$ declare -A ass_array01
thanlon@thanlon-master:~$ ass_array01[name]=thanlon
thanlon@thanlon-master:~$ ass_array01[age]=23
thanlon@thanlon-master:~$ echo ${ass_array01[name]}
thanlon
thanlon@thanlon-master:~$ echo ${ass_array01[age]}
23
```
一次赋多个值：
```shell
thanlon@thanlon-master:~$ declare -A ass_array2
thanlon@thanlon-master:~$ ass_array2=([name]=thanlon [age]=23)
thanlon@thanlon-master:~$ echo ${ass_array2[name]}
thanlon
thanlon@thanlon-master:~$ echo ${ass_array2[age]}
23
```
3）查看数组
```shell
thanlon@thanlon-master:~$ declare -A
……
declare -A ass_array01=([age]="23" [name]="thanlon" )
declare -A ass_array2=([age]="23" [name]="thanlon" )
```
4）访问数组元素
```shell
echo ${ass_array[index]} # 访问数组某个索引的值
echo ${ass_array[@]} 		# 访问数组中所有元素，等价于echo ${array[*]}
echo ${#ass_array[@]} 		# 获取数组的个数
echo ${!ass_array[@]} 		# 获取数组元素的索引
```
5）遍历数组

对于关联数组，**`需要通过数组元素的索引值进行遍历，不能通过数组元素的编号进行遍历`**：
```shell
thanlon@thanlon-master:~$ echo ${ass_array2[name]}
thanlon
thanlon@thanlon-master:~$ echo ${ass_array2[age]}
23
```

###### 6.4 职员信息查询系统
`employee_info.sh：`
```shell
#!/usr/bin/bash
#Description：
#Author: thanlon@sina.com
#Realease：1.0
#Create Time：2020/04/12 12:37
for((i=0;i<3;i++))
        do
                read -p "输入第$((i+1))个职员的人名：" employee_name[$i]
                read -p "输入第$[$i+1]个的职员年龄：" employee_age[$i]
                read -p "输入第`expr $i + 1`个职员的性别：" employee_gender[$i]
                echo
done
clear
echo -e "\t\t\t\t职员信息查询系统"
echo "友情提示：输入Q可以直接退出系统！"
while :
        do
                read -p "输入要查询的职员的姓名：" name
                [ $name == "Q" ]&& exit
                flag=0
                for((i=0;i<3;i++))
                        do
                                if [ "$name" == "${employee_name[$i]}" ];then
                                        echo "职员姓名：${employee_name[$i]} 职员年龄：${employee_age[$i]} 职员性别：${employee_gender[$i]}"
                                        flag=1
                                fi
                done
                [ $flag -eq 0 ]&&echo "抱歉，没有找到该职员！"
                echo
done
```
`执行过程：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412134830817.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412134928175.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)