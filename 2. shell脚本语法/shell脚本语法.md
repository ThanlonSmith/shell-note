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