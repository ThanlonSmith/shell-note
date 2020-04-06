##### 5. shell变量
###### 5.1 变量介绍
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在编程中，我们总有一些数据存放在内存以待后续使用时快速取出来。内存在系统启动的时候被按照1B一个单位编号（16进制编号），并对内存的使用情况做记录，保存在内存跟踪表中。
>**变量是编程中最常用的一种临时在内存中存取数据的一种方式。**
###### 5.2 变量分类
① 本地变量：用户私有变量，只有本用户才可以使用，保存在家目录下的 **.bash_profile** 或者 **.bashrc**文件中。**`.bash_profile中会加载.bashrc`** 。

② 全局变量：所有用户都可以使用，保存在 **/etc/profile** 或者 **/etc/bashrc**，其中 **`profile会加载bashrc`**，全局变量的生命周期是计算机开机到关机。

③ 用户自定义变量：用户自定义的变量，如终端中写的临时变量，只作用于本终端。还有脚本中定义的变量作用于脚本执行的时候，这些都是用户自定义变量。
>**本地变量会在登录成功以后，把变量从文件中加载到内存。而全局变量是在用户登录之前，把所有变量从文件中加载到内存。**
###### 5.3 变量管理
1）定义变量

① 变量的格式是：变量名=值，**`在shell变成中变量名和等号之间不能有空格。`**

② 变量的命名规则：
- 只能使用英文字母、数字、下划线，首个字符不能是数字
- 中间不能有空格，可以使用下划线
- 不能使用标点符号
- 不能使用bash里的关键字
>**字符串要使用单引号或者双引号引起来，可以使用help命令查看保留的关键字。`shell区分大小写，可以把变量名写成大写，就不会和命令冲突了。`**

2）取消变量

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;可以在 **.bashrc**中定义私有变量，然后使用source命令将私有变量加载到内存中，最后使用 **`unset`** 命令取消变量，也就是把变量销毁，释放内存空间。注意前面说过在 **.bashrc**中定义的变量会在下次用户登录成功之后，加载到内存中。
```shell
# 编辑.bashrc文件，在文件最后加上：MYSITE='www.thanlon.cn'  
thanlon@thanlon-master:~$ vim ~/.bashrc
# 输出这个变量，因为还没有加载到内存，所以不存在
thanlon@thanlon-master:~$ echo $MYSITE

# 将设置的变量加载到内存
thanlon@thanlon-master:~$ source .bashrc 
# 输出设置的变量MYSITE
thanlon@thanlon-master:~$ echo $MYSITE
www.thanlon.cn
# 取消变量
thanlon@thanlon-master:~$ unset MYSITE
# 检查变量是否还在内存中，发现已不存在
thanlon@thanlon-master:~$ echo $MYSITE

thanlon@thanlon-master:~$
```
>**注意：unset后面直接跟变量名，不要加上$符号。**

3）定义全局变量
```shell
# 编辑/etc/profile
thanlon@thanlon-master:~$ sudo vim /etc/profile
# 在末尾加上下面给的内容（设置一个全局变量）
export MYSITE='www.thanlon.com'
# 加载到内存
thanlon@thanlon-master:~$ source /etc/profile
# 输出变量
thanlon@thanlon-master:~$ echo $MYSITE
www.thanlon.com
```
>**注意：加了export，$MYSITE就是一个全局变量，计算机开机就被加载到内存中。但是如果不加export，那么 $MYSITE 就是一个本地用户变量，在切换用户后变量就没有了！`如果在/etc/profile中设置了全局变量(不加export)，在.bashrc也设置了同名的变量，那么谁最后加载到内存(source)，这个变量就是谁中配置的`。**