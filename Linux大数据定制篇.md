# 大数据定制篇

## shell编程

##### 为什么要学习shell编程

1. Linux运维工程师在进行服务器集群管理时，需要编写Shell程序来进行服务器管理。
2. 对于JavaEE和Python程序员来说，工作的需要，你的老大会要求你编写一些Shell脚本进行程序或者是服务器的维护，比如编写一个定时备份数据库的脚本。
3. 对于大数据程序员来说，需要编写Shell程序来管理集群。

##### shell是什么

Shell是一个命令行解释器，它为用户提供了一个向Linux内核发送请求以便运行程序的界面系统级程序，用户可以用Shell来启动、挂起、停止甚至是编写一些程序。

![image-20210808152957642](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808152957642.png)

#### shell脚本的执行方式（快速入门）

##### 脚本格式要求

1. 脚本以#!/bin/bash开头
2. 脚本需要有可执行权限

案例：编写一个shell脚本，输出hello world

1. 首先创建一个shell脚本

`vim hello.sh`

2. 然后在脚本中输入

   `#!/bin/bash`

   `echo "hello,world!"`

3. 执行方式

   1. 输入脚本的绝对路径或相对路径

      首先要赋予hello.sh脚本的+x权限（执行权限）

      执行脚本（采用的是相对路径，也可以采用/root/shell/hello.sh绝对路径执行）

      ![image-20210808154803108](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808154803108.png)

   2. sh＋脚本（不推荐）

      不用赋予脚本+x权限，直接执行即可

      ![image-20210808155012043](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808155012043.png)

### shell的变量

介绍

Linux shell中的变量分为系统变量和用户自定义变量

##### 系统变量

例如

- $HOME
- $PWD
- $SHELL
- $USER

![image-20210808155536035](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808155536035.png)

![image-20210808155515342](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808155515342.png)

显示当前shell中所有变量：set

##### shell变量的定义

基本语法

1. 定义变量，变量=值
2. 撤销变量，unset 变量
3. 声明静态变量：readonly 变量，注意：不能unset

+ 案例1，定义变量A

  > 注意：在定义变量时不能有空格，否则会默认定义的变量为命令符

  > 输出（print）用的操作符为echo，如果要输出变量，则需在前面加上“$“

  ![image-20210808160323024](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808160323024.png)

+ 案例2，声明静态的变量B，不能unset

  ![image-20210808160703084](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808160703084.png)

+ 案例3，将变量提升为全局环境变量，可供其他shell程序使用

##### 变量定义的规则

1) 变量名称可以由字母、数字和下划线组成，但是不能以数字开头。
2) 等号两侧不能有空格
3) 变量名称一般习惯为大写

##### 将命令的返回值赋给变量（重点）

1. `A=ls -la` 反引号，运行里面的命令，并把结果返回给变量A
2. A=$(ls -la) 等价于反引号

![image-20210808161558303](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808161558303.png)

![image-20210808161624099](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808161624099.png)

#### 设置环境变量

##### 基本语法

1) export 变量名=变量值（功能描述：将shell变量输出为环境变量）
2) source 配置文件（功能描述：让修改后的配置信息立即生效）
3) echo $变量名（功能描述：查询环境变量的值）

理解

![image-20210808162138090](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808162138090.png)

###### 案例

1) 在/etc/profile文件中定义TOMCAT_HOME环境变量
2) 查看环境变量TOMCAT_HOME的值
3) 在另外一个shell程序中使用TOMCAT_HOME

在/etc/profile文件的末尾添加

```shell
#定义一个自己的环境变量
TOMCAT_HOME=/opt/tomcat
export TOMCAT_HOME
```



```shell
#多行注释
:<<!
要注释掉的内容
!
#使用我们自定义的环境变量
echo "tomcat_home=$TOMCAT_HOME"
```

#### 位置参数变量

###### 基本介绍

当我们执行一个shell脚本时，如果希望获取到命令行的参数信息，就可以使用到位置参数变量
比如：./myshell.sh 100 200 , 这个就是一个执行shell的命令行，可以在myshell 脚本中获取到参数信息

###### 基本语法

$n 功能描述：n为数字，0表示命令本身，1-9表示第一到第九个参数，10以上的参数需要用大括号包含

$* 这个变量代表命令行中所有的参数，把所有的参数看成一个整体

$@ 这个变量也代表命令行中所有的参数，但是把每个参数区分对待

$# 代表命令行中所有参数的个数

![image-20210808203516784](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808203516784.png)

![image-20210808203604139](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808203604139.png)

#### 预定义变量

就是shell设计者事先已经定义好的变量，可以直接在shell脚本中使用

###### 基本语法

+ $$ 当前进程的进程号（PID）
+ $! 后台运行的最后一个进程的进程号（PID）
+ ＄？最后一次执行的命令的返回状态，如果这个变量的值为０，则说明上述命令没有正确执行，如果这个变量的值非０，则证明上述命令执行正确了

###### 案例

![image-20210808211707413](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808211707413.png)

![image-20210808211738714](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210808211738714.png)

### 运算符

###### 基本语法

1. “$((运算式))”

   或“$​[运算式]”

2. expr m + n
    **注意expr运算符间要有空格**

3. expr m -n

4. expr \*, /, % 乘，除，取余

###### 案例

+ 计算(2+3)×4

  方式1：使用$((运算式))

  ![image-20210809085159877](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809085159877.png)

  ![image-20210809085136295](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809085136295.png)

  方式2：使用$[运算式]（推荐）

  ![image-20210809085441552](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809085441552.png)

  方式3：使用expr（注意要加上反引号`）

  ![image-20210809091040604](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809091040604.png)

+ 求出两个参数之和

  ![image-20210809091346067](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809091346067.png)

### 条件判断

#### 判断语句

###### 基本语法

[ condition ] （**注意condition前后都要有空格**）

#非空返回true，可以用$?验证

###### 判断语句

- 两个整数的比较

  = 字符串比较
  -lt 小于
  -le 小于等于
  -eq 等于
  -gt 大于
  -ge 大于等于
  -ne 不等于

- 按照文件权限进行判断

  -r 有读的权限
  -w 有写的权限
  -x 有执行的权限

- 按照文件类型进行判断

  -f 文件存在并且是一个常规的文件
  -e 文件存在
  -d 文件存在并是一个目录

###### 应用实例

1. 判断“ok”是否等于“ok”

   ![image-20210809092238163](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809092238163.png)

2. 判断23是否≥22

   ```shell
   if [23 -gt 22]
   then
   	echo "大于"
   fi
   ```

3. /root/shell目录中的文件是否存在

   ```shell
   if [ -e /root/shell/aaa.txt ]
   then
   	echo "存在"
   fi
   ```

   ![image-20210809093119995](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809093119995.png)

### 流程控制

#### if判断

###### 基本语法

第一种形式

```shell
if[ 条件判断式 ]
then
	程序
fi
```

第二种形式

```shell
if [ 条件判断式 ]
then
	程序
elif [ 条件判断式 ]
then
	程序
fi
```

注意：在条件判断式中括号和条件判断之间必须有空格

###### 案例

```shell
if[ $1 -ge 60 ]
then
	echo "及格了"
elif [ $1 -lt 60 ]
then
	echo "不及格"
fi
```

#### case语句

###### 基本语法

case $变量名 in
"值1"）
如果变量的值等于值1，则执行程序1
;;
"值2"）
如果变量的值等于值2，则执行程序2
;;
…省略其他分支…
*）
如果变量的值都不是以上的值，则执行此程序
;;
esac

###### 案例

当命令行参数是1 时，输出"周一", 是2 时，就输出"周二"，其它情况输出"other"

```shell
case $1 in
"1")
echo "周一"
;;
"2")
echo "周二"
;;
*)
echo "other"
;;
esac
```

#### for循环

##### 基本语法1

```shell
for 变量 in 值1 值2 值3…
do
	程序
done
```

###### 案例：打印命令行输入的参数

```shell
#方式1：使用$*
for i in "$*"
do
	echo "the number is $i"
done
```

输出

![image-20210809103500450](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809103500450.png)

```shell
#方式2：使用$@
for i in "$@"
do
	echo "the number is $i"
done
```

输出

![image-20210809103753897](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809103753897.png)

##### 基本语法2

```shell
for ((初始值; 循环控制条件; 变量变化))
do
	程序
done
```

###### 案例：从1加到100的值显示

![image-20210809104354224](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809104354224.png)

#### while循环

##### 基本语法1

```shell
while[ 条件判断式 ]
do
	程序
done
```

###### 案例

![image-20210809104949117](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809104949117.png)

### 读取控制台输入

`read(选项)(参数)`

选项

-p：指定读取值时的提示符；
-t：指定读取值时等待的时间（秒），如果没有在指定的时间内输入，就不再等待了

###### 案例

![image-20210809110831917](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809110831917.png)

### 函数

shell编程和其它编程语言一样，有系统函数，也可以自定义函数。系统函数中，我们这里就介绍两个。

#### 系统函数

##### basename基本语法

###### 功能：

返回完整路径最后/ 的部分，常用于获取文件名
`basename [pathname] [suffix]`
`basename [string] [suffix]`

（功能描述：basename命令会删掉所有的前缀包括最后一个（‘/’）字符，然后将字符串显示出来。

###### 选项：

suffix为后缀，如果suffix被指定了，basename会将pathname或string中的suffix去掉。

###### 案例

![image-20210809112654576](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809112654576.png)

##### dirname基本语法

功能：返回完整路径最后/前面的部分，常用于返回路径

`dirname 文件绝对路径`

（功能描述：从给定的包含绝对路径的文件名中去除文件名（非目录的部分），然后返回剩下的路径（目录的部分））

###### 案例

![image-20210809112953457](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809112953457.png)

#### 自定义函数

###### 基本语法

```shell
[ function ] funname[()]
{
	Action;
	[return int;]
}
```

调用直接写函数名：funname [ 值 ]

![image-20210809113956135](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809113956135.png)

### shell编程综合案例

###### 需求

1. 每天凌晨2:10 备份数据库atguiguDB 到/data/backup/db
2. 备份开始和备份结束能够给出相应的提示信息
3. 备份后的文件要求以备份时间为文件名，并打包成.tar.gz 的形式，比如：
   2018-03-12_230201.tar.gz

4) 在备份的同时，检查是否有10天前备份的数据库文件，如果有就将其删除。

###### 思路分析

![image-20210809151514694](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210809151514694.png)
