# Linux实操篇-6

### 网络配置基本原理

NAT模式原理图

![image-20210807205500341](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210807205500341.png)

##### 查看网络IP和网关

使用ping指令测试主机之间的连通性

语法：`ping 目的主机`

### Linux网络环境配置

- 第一种方式：自动获取

  缺陷：每次得到的IP地址都不一样

- 第二种方式：指定固定的IP

  网络配置文件：`/`etc/sysconfig/network-scripts/ifcfg-ens33/

![image-20210807212849138](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20210807212849138.png)

## 进程管理

#### 进程的基本介绍

在LINUX中，每个执行的程序（代码）都称为一个进程。每一个进程都分配一个ID号。

每一个进程，都会对应一个父进程，而这个父进程可以复制多个子进程。例如www服务器。

每个进程都可能以两种方式存在的。前台与后台，所谓前台进程就是用户目前的屏幕上可以进行操作的。后台进程则是实际在操作，但由于屏幕上无法看到的进程，通常使用后台方式执行。

一般系统的服务都是以后台进程的方式存在，而且都会常驻在系统中。直到关机才才结束。

#### 显示系统执行的进程

ps命令是用来查看目前系统中，有哪些正在执行，以及它们执行的状况。
可以不加任何参数.

*ps显示的信息选项*

| 字段 | 说明                     |
| ---- | ------------------------ |
| PID  | 进程识别号               |
| TTY  | 终端机号                 |
| TIME | 此进程消耗的CPU时间      |
| CMD  | 正在执行的命令或者进程名 |

ps -a 显示当前终端的所有进程信息

ps -u 以用户的格式显示进程信息

ps -x 显示后台进程运行的参数

###### ps详解

1. 指令：ps –aux|grep xxx ，比如我看看有没有sshd服务
2. 指令说明
   •System V展示风格
   •USER：用户名称
   •PID：进程号
   •%CPU：进程占用CPU的百分比
   •%MEM：进程占用物理内存的百分比
   •VSZ：进程占用的虚拟内存大小（单位：KB）
   •RSS：进程占用的物理内存大小（单位：KB）
   •TT：终端名称,缩写.
   •STAT：进程状态，其中S-睡眠，s-表示该进程是会话的先导进程，N-表示进程拥有比普通优先级更低的优先级，R-正在运行，D-短期等待，Z-僵死进程，T-被跟踪或者被停止等等
   •STARTED：进程的启动时间
   •TIME：CPU时间，即进程使用CPU的总时间
   •COMMAND：启动进程所用的命令和参数，如果过长会被截断显示

•ps -ef是以全格式显示当前所有的进程
•-e 显示所有进程。-f 全格式。
•ps -ef|grep xxx
•是BSD风格
•UID：用户ID
•PID：进程ID
•PPID：父进程ID
•C：CPU用于计算执行优先级的因子。数值越大，表明进程是CPU密集型运算，执行优先级会降低；数值越小，表明进程是I/O密集型运算，执行优先级会提高
•STIME：进程启动的时间
•TTY：完整的终端名称
•TIME：CPU时间
•CMD：启动进程所用的命令和参数

### 终止进程kill和killall

若是某个进程执行一半需要停止时，或是已消了很大的系统资源时，此时可以考虑停止该进程。使用kill命令来完成此项任务。

`kill [选项] 进程号`

通过进程号杀死进程

`killall 进程名称`

通过进程名杀死进程，也支持通配符

强制杀掉一个终端：想要强制终止某个终端，需要使用 `kill -9 进程号`

### 查看进程树pstree

`pstree [选项]`

可以更加直观地来看进程信息

常用选项

-p :显示进程的PID

-u :显示进程的所属用户

### 服务管理

服务(service) 本质就是进程，但是是运行在后台的，通常都会监听某个端口，等待其它程序的请求，比如(mysql , sshd 防火墙等)，因此我们又称为守护进程，是Linux中非常重要的知识点。

##### service管理指令

service 服务名[start | stop | restart | reload | status]
在CentOS7.0后不再使用service ,而是systemctl

案例：查看防火墙状态(CentOS 7.0)

`systemctl status firewalld`

查看系统有哪些服务

`ls -l /etc/init.d/`

##### 服务的运行级别

查看或修改默认的运行级别

`vi /etc/inittab`

通过chkconfig命令对每个服务的各个运行级别设置自启动/关闭

### 动态监控进程

#### 监控网络状态

基本语法：`top [选项]`

top与ps命令很相似。它们都用来显示正在执行的进程。Top与ps最大的不同之处，在于top在执行一段时间可以更新正在运行的的进程。

| 选项    | 功能                                       |
| ------- | ------------------------------------------ |
| -d 秒数 | 指定top命令每隔几秒更新，默认是3秒         |
| -i      | 使top不显示任何闲置或僵死进程              |
| -p      | 通过指定监控进程ID来仅仅监控某个进程的状态 |

输入u然后可以指定查看的用户

输入q可以退出

#### 查看系统网络情况netstat

基本语法 `netstat[选项]`

`netstat -anp`

说明：

- -an 按照一定的顺序排列输出
- -p 显示哪个进程在调用

### RPM包管理

一种用于互联网下载包的打包及安装工具，它包含在某些Linux分发版中。它生成具有.RPM扩展名的文件。RPM是RedHat Package Manager（RedHat软件包管理工具）的缩写，类似windows的setup.exe，这一文件格式名称虽然打上了RedHat的标志，但理念是通用的。

查询已经安装的rpm列表：`rpm -qa | grep xx`

案例：查询Linux虚拟机中是否安装Firefox

`rpm -qa | grep firefox`

##### 常用查询指令

rpm -qa :查询所安装的所有rpm软件包
rpm -qa | more
rpm -qa | grep X [rpm -qa | grep firefox ]
rpm -q 软件包名:查询软件包是否安装
rpm -q firefox
rpm -qi 软件包名：查询软件包信息
rpm -qi file
rpm -ql 软件包名:查询软件包中的文件
rpm -ql firefox
rpm -qf 文件全路径名查询文件所属的软件包
rpm -qf /etc/passwd
rpm -qf /root/install.log

##### 卸载软件包

`rpm -e [软件名]`

如果要强制删除（不推荐）

`rpm -e --nodeps foo`

#####  安装软件

`rpm -ivh [rpm包全路径名称]`

参数说明

- i=install 安装
- v=verbose 提示
- h=hash 进度条

实例（安装火狐）

先找到firefox的安装rpm包，需要挂载上安装centos的ISO文件，然后到/media/下找到

### yum

Yum 是一个Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包。

基本指令

- 查询yun服务器是否有需要安装的软件

  `yum list | grep xx软件列表`

- 安装指定的yum包

  `yum install xxx 下载安装`

  
