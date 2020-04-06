##### 3. 格式化输出
###### 3.1 格式化输出命令echo
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;一个程序有0个或0个以上的输入，有一个或一个以上的输出。格式化输出命令是<kbd>echo</kbd>，它的功能是将内容输出到默认的显示设备中，**`一般起到提示的作用!`** echo默认会将输出的字符串送到标准输出，输出的字符串之间用空白字符隔开，并在最后加上换行号。命令选项：
| -n               | -e                                                           |
| ---------------- | ------------------------------------------------------------ |
| 不在最后自动换行 | **`若字符串出现需要转义的字符，需要特别加以处理`**，不会将转义字符当做一般字符输出。 |
```py
thanlon@thanlon-master:~$ echo "Login:";read
Login:
thanlon
thanlon@thanlon-master:~$ echo -n "Login:";read
Login:thanlon
thanlon@thanlon-master:~$ echo "date:";date +%F;
date:
2020-04-02
thanlon@thanlon-master:~$ echo -n "date:";date +%F;
date:2020-04-02
```
转义字符：
| \a         | \b             | \c                                   | \f                           | \n                   | \r                         | \t      | \v       | \         | \nnn                             |
| ---------- | -------------- | ------------------------------------ | ---------------------------- | -------------------- | -------------------------- | ------- | -------- | --------- | -------------------------------- |
| 发出警告声 | 删除前一个字符 | 最后不加上换行符号，与命令选项-n相同 | 换行但光标仍停留在原来的位置 | 换行且光标移动到行首 | 管标移动到首行，但是不换行 | 插入tab | 与\f相同 | 插入\字符 | 插入nnn(八进制)所代表的ASCII字符 |
`常用的转义转义字符 \a:`
```bash
thanlon@thanlon-master:~$ echo "\a\a\a\a\a"
\a\a\a\a\a
thanlon@thanlon-master:~$ echo -e "\a\a\a\a\a"

thanlon@thanlon-master:~$ 
```
`常用的转义字符 \t:`

```bash
thanlon@thanlon-master:~$ echo "thanlon"
thanlon
thanlon@thanlon-master:~$ echo -e "\tthanlon"
	thanlon
```
`常用的转义字符 \n:`
```bash
thanlon@thanlon-master:~$ echo "\n"
\n
# echo本身输出一个换行，所有有两次换行
thanlon@thanlon-master:~$ echo -e "\n"


thanlon@thanlon-master:~$ 
```
`常用的转义字符 \b:`
```bash
# 必须在同一行才能删除（不太确定是在转义之前输出了换行）
thanlon@thanlon-master:~$ echo -e "a\b"
a

thanlon@thanlon-master:~$ echo -e -n "a\b"
thanlon@thanlon-master:~$ 
```
`常用的转义字符 \c:`
```bash
thanlon@thanlon-master:~$ echo -e "thanlon\c"
thanlonthanlon@thanlon-master:~$ echo -n "thanlon"
thanlonthanlon@thanlon-master:~$ echo -n "thanl\con"
thanl\conthanlon@thanlon-master:~$ echo -e "thanl\con"
```
`应用1：倒计时脚本 time.sh：`

```bash
#!/usr/bin/bash
# Author：thanlon@sina.com
# Create Time：2020/04/02 14:21
# Release：1.0
# Script Description：countdowm script
for time in `seq 9 -1 0`;do
        echo -n -e "\b$time秒"
        sleep 1
done
echo
```
`应用2：写一个水果商店的脚本，fruits_shop.sh：`
```bash
#!/usr/bin/bash
# Author：thanlon@sina.com
# Create Time：2020/04/02 14:21
# Release：1.0

echo -e "\t\tFruits Shop"
echo -e "\t1) Apple"
echo -e "\t2) Orange"
echo -e "\t3) Banana"
echo -n "Which do you chose: "
read
```
`执行fruits_shop.sh输出记录：`

```bash
thanlon@thanlon-master:~$ bash fruits_shop.sh
		Fruits Shop
	1) Apple
	2) Orange
	3) Banana
Which do you chose:
```