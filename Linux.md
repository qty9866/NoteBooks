# Linux

## 1,计算机硬件软件体系

### 1.1 冯诺依曼体系结构

- 计算机处理的数据和指令一律用二进制数表示
- 计算机硬件由运算器、控制器、存储器、输入设备、输出设备五大部分组成

### 1.2 计算机硬件组成

- 输入设备
  - 输入设备用来将人们熟悉的信息形式转换为机器能够识别的信息形式
    - 常见的有键盘、鼠标等
- 输出设备
  - 输出设备可以将机器运算结果转换为人们熟悉的信息格式
  - 打印机、显示器等等
- 存储器 
  - 存储器用来存放数据和程序 
  - RAM(random access memory）即随机存储内存:
    -  速度快，容量小 
    -  掉电易失 
    -  逻辑IO 
  - ROM（Read-Onboy Memory）即只读内存 硬盘: 
    - 容量大，速度相对较慢 
    - 长久保存
    - 物理IO
- CPU(中央处理器) 控制器 
  - 控制器运算器 
    - 主要用来控制和指挥程序和数据的输入运行，以及处理运算结果 
  - 运算器
    - 主要运行算数运算和逻辑运算，并将中间结果暂存到运算器中

### 1.3 硬盘的分类

- 硬盘按照**存储介质**的不同可以分为如下两种
  - **机械硬盘**（Hard Disk Driver, HDD）
    - 机械硬盘采用磁性碟片来存储数据 
    - 用显微镜把盘片放大，会看见盘片表面凹凸不平，凸起的地方被磁化，凹的地方是没有被磁化
    - 凸起的地方代表数字1（磁化为1），凹的地方代表数字0。 
    - 硬盘可以以二进制来存储表示文字、图片等信息。 
    - 硬盘可以根据转速来判断硬盘的好坏 7200转/分 100-200M/s
  - **固态硬盘**（Solid State Disk, SSD）
    -  固态硬盘通过闪存颗粒（固态电子存储芯片阵列）来存储数据
- **读写速度的区别** 
  - 固态硬盘的读取速度普遍可以达到400M/s，写入速度也可以达到130M/s以上
  - 其读写速度是普通机械硬盘的3-5倍。
- **机械硬盘的数据读写**
  -  主流的硬盘半机械半电子硬盘(机械硬盘) 
     - 硬盘的转速(转速越快读取越快) 
     - 寻道时间 
     - 数据传输时间

### 1.4 网络连接概念 

- **`IP`地址`IPADDR`** 
  - `IP`地址是一种逻辑地址，用来标识网络中一个个主机
    -  `IP`地址=网络地址+主机地址
    -  `IP`地址是一个 4 * `8bit`（1字节）由 0/1 组成的数字串（`IP4`协议）
- **子网掩码`NETMASK`**
  - 子网掩码只有一个功能，就是将IP地址划分为网络地址和主机地址两部分。
  - 子网掩码用来判断任意两台计算机的`IP`地址是否在同一个子网中的根据
    - A 192.168.7.111 B 192.168.8.222
    - 255.255.0.0
- **默认网关`GATEWAY`**
  - 连接两个不同的网络的设备都可以叫网关设备；网关的作用就是实现两个网络之间进行通讯与 控制。 
  - 网关地址就是网关设备的IP地址
- **域名服务器`DNS`** 
  - `DNS`是域名服务器，用来解析域名的（域名和`IP`之间的解析）。
  - 如果没有这东西，登陆某个网站时就必须输入该网站的`IP`地址，有了`DNS`就可以直接输入网 址。

### 1.5网络连接模式 

- **`host-onboy`(主机模式)** 
  - 在某些特殊的网络调试环境中，要求将真实环境和虚拟环境隔离开，这时你就可采用`hostonboy`模式。
  - 在`host-onboy`模式中，所有的虚拟系统是可以相互通信的，但虚拟系统和真实的网络是被隔 离开的。 
  - 在`host-onboy`模式下，虚拟系统的`TCP/IP`配置信息都是由`VMnet1`(`host-onboy`)虚拟网络的 `DHCP`服务器来动态分配的
- **bridged(桥接模式)**
  -  `VMWare`虚拟出来的操作系统就像是局域网中的一台独立的主机，它可以访问网内任何一台机 器。
  -  使用桥接模式的虚拟系统和宿主机器的关系，就像连接在同一个Hub上的两台电脑。 
  -  当前主机`IP` 为 192.168.8.100 虚拟机 `192.168.8.xxx` 学习期间为了防止`IP`冲突，所以不选择这种模式
- **NAT(网络地址转换模式)**
  - 使用NAT模式，就是让虚拟系统借助NAT(网络地址转换)功能，通过宿主机器所在的网络来访 问公网。
  - NAT模式下的虚拟系统的`TCP/IP`配置信息是由`VMnet8`(NAT)虚拟网络的`DHCP`服务器提供的 
  - 虚拟系统也就无法和本局域网中的其他真实主机进行通讯

### 1.6 软件分类

- **应用软件** 
  - 就是为了实现某些业务功能
  - 应用软件要基于对应的系统软件 
    - 不同的操作系统要安装不同的软件 
- **系统软件** 
  - 就是为了和硬件打交道 
  - 屏蔽应用软件与硬件的差异

- 系统软件的分类
  -  Window 用户量全球最大 收费，不开源，民用较多 各种软件比较齐全
  -  Mac 只限定于某些苹果的品牌机 ios--自成一家 
  -  GNU/Linux GNU是一个开源软件组织,世界上所有的软件都应该开源免费
     -  GNU Is Not Unix 
     -  `GCC`++ 
     -  托瓦兹 林纳斯 Linus -- Linux(Linux is not unix) 
     -  Logo是企鹅

### 1.7 Linux分支

- **`RedHat`（收费）**
  -  `CentOS` 完全开源免费 
  -  不要使用最新版的`CentOS` 
  -  主要用于服务器版本
- `Debain`（免费） 
  - `Ubuntu` 
    - 视窗界面良好的Linux系统 
    - 一些主流的软件都支持`Ubuntu`系统

## 2.虚拟机安装与配置

### 2.1. 虚拟化技术 

- 可以更好的利用计算机闲置的资源 
- 我们可以在计算机中虚拟出多台虚拟机帮助我们执行程序或者业务 
- 虚拟机的各种组成理论上和真实主机是一样的
- 如果要使用这种技术只需要安装对应的软件即可

### 2.2 虚拟机的安装

安装完成CentOS7后，对网卡进行配置：

```shell
[root@basenode ~]# vi /etc/sysconfig/network-scripts/ifcfg-ens33 
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
DEVICE=ens33
ONBOOT=yes
IPADDR=192.168.88.110
NETMASK=255.255.255.0
GATEWAY=192.168.88.2
DNS1=114.114.114.114
# 保存之后，重启网卡
[root@basenode ~]# systemctl restart network.service
# 测试网络
[root@basenode ~]# ping www.baidu.com
PING www.baidu.com (36.152.44.96) 56(84) bytes of data.
64 bytes from 36.152.44.96 (36.152.44.96): icmp_seq=1 ttl=128 time=5.81 ms
64 bytes from 36.152.44.96 (36.152.44.96): icmp_seq=2 ttl=128 time=7.28 ms
64 bytes from 36.152.44.96 (36.152.44.96): icmp_seq=3 ttl=128 time=6.24 ms
64 bytes from 36.152.44.96 (36.152.44.96): icmp_seq=4 ttl=128 time=36.4 ms
64 bytes from 36.152.44.96 (36.152.44.96): icmp_seq=5 ttl=128 time=8.28 ms
64 bytes from 36.152.44.96 (36.152.44.96): icmp_seq=6 ttl=128 time=7.36 ms
--- www.baidu.com ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 14025ms
rtt min/avg/max/mdev = 5.812/11.912/36.478/11.015 ms
```

#### 2.2.1 **防火墙**

- 保护本机的端口不被别人访问
- 如果端口需要被别人访问到，需要添加端口的防火墙例外
- 关闭防火墙
  - 本次开机状态下防火墙关闭
    - systemctl stop firewalld (本次服务内关闭防火墙)
  - 服务器重启后防火墙禁用
    - systemctl disable firewalld(禁用防火墙服务)

#### 2.2.2 **软件安装限制**

- 操作系统对未知软件的安装有可能拒绝或者警告，我们需要禁用这个功能

  - ```shell
    vi /etc/selinux/config
    
    SELINUX=disabled
    ```

    

#### **2.2.3 关机**

- 关机

  - `halt`
    - 直接拔掉电源

  - `poweroff`
    - 直接关闭机器，但是有可能当前虚拟机其他人在使用

  - `shutdown -h now`
    - 马上关闭计算机 ，但是可以给其他用户发送消息

  - `reboot`
    - 重启虚拟机

### 2.3 **快照与克隆**

- 拍摄快照

  - 记录当前虚拟机的状态

  - 拍摄快照的时候一定要关机

- 转到
  - 回到某一个历史快照的节点

- 克隆

  - 复制某一个历史快照节点

  - 克隆的方式

    - 链接克隆

      - 当前节点文件夹只存储差异性数据

      - 相同数据存放在原始节点上

      - 优点：节省硬盘空间 缺点：耦合性大

    - 完整克隆

      - 就是基于原始节点完全拷贝到新节点的文件夹中

      - 优点：耦合性抵 缺点：硬盘空间使用大

      - 推荐使用完整克隆



## 3. Linux的命令

### 3.1 命令学习法

- **Linux命令与参数之间必须用空格隔开**

- **Linux命令是区分大小写的**

- **如果输入了错误的命令**

  - -bash: abcd: command not found

  - 命令敲错了
  - 命令未安装

- **type 命令的类型**

  ```shell
  - cd is a shell builtin
  
  - ping is /bin/ping
  
  - ll is aliased to `ls -l --color=auto'
  
  - for is a shell keyword
  
  - cd is a shell builtin
  ```

  - help
    - 内置命令的帮助文档
  - man
    - 外部命令的帮助文档
    - 因为当前系统为minimal的，very basic 没有man
    - 包需要手动安装man
      - `yum install man man-pages -y`
  - 将来工作中如果遇到生疏的命令，直接百度
    - 如果不是为了装C,完全没必要查看命令手册

### 3.2 常用的命令

- `whereis` 查询命令文件的位置

  ```shell
  [root@basenode ~]# whereis ping
  ping: /usr/bin/ping /usr/share/man/man8/ping.8.gz
  ```

- `file` 查看文件的类型

  ```shell
  [root@basenode ~]# file /usr/bin/cd
  /usr/bin/cd: POSIX shell script, ASCII text executable
  ```

- `who` 查看当前在线的用户

  ```shell
  [root@basenode ~]# who
  root     pts/0        2022-08-23 17:18 (192.168.88.1)
  ```

- `whoami` 我是谁

  ```shell
  [root@basenode ~]# whoami
  root
  ```

- `pwd` 我在那

  ```shell
  [root@basenode ~]# pwd
  /root
  ```

- `uname -a` 查看内核信息

  ```shell
  [root@basenode ~]# uname -a
  Linux basenode 3.10.0-1160.el7.x86_64 #1 SMP Mon Oct 19 16:18:59 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
  ```

- `echo` 类似于 `sout syso ，`打印语句

  ```
  [root@basenode ~]# echo hello hud
  hello hud
  ```

- `clear` 清屏

- `history` 历史

  ```shell
  [root@basenode ~]# history
      1  systemctl disable firewalld
      2  status firewalld
      3  systemctl status firewalld
      4  systemctl stop firewalld
      5  systemctl status firewalld
      6  vi /etc/selinux/config
      7  poweroff
      8  ip addr
      9  mna
     10  man
     11  ll
     12  ifconfig
     13  yum search ifconfig
     14  ifconfig
     15  de type
     16  cd type
     17  type cd
     18  type ls
     19  whisis ping
     20  whereis ping
     21  file /usr/bin/ping
     22  file /usr/bin/cd
     23  who
     24  whoami
     25  pwd
     26  uname -a
     27  echo hello hud
     28  history
  # 可以看到历史敲的指令，如果不想被看到可以使用history -c
  [root@basenode ~]# history -c
  [root@basenode ~]# history
      1  history
  ```

  

### **3.3.** **特殊字符**

- **.点：**

  - 如果文件的开始是.说明当前文件是一个隐藏文件
  - . 指向当前目录
  - ..指向当前目录的上级目录

  ```shell
  #带点的就是隐藏文件
  [root@basenode ~]# ll -al
  total 28
  dr-xr-x---.  2 root root  135 Aug 23 01:08 .
  dr-xr-xr-x. 17 root root  244 Aug 23 04:11 ..
  -rw-------.  1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
  -rw-------.  1 root root  245 Aug 23 07:37 .bash_history
  -rw-r--r--.  1 root root   18 Dec 29  2013 .bash_logout
  -rw-r--r--.  1 root root  176 Dec 29  2013 .bash_profile
  -rw-r--r--.  1 root root  176 Dec 29  2013 .bashrc
  -rw-r--r--.  1 root root  100 Dec 29  2013 .cshrc
  -rw-r--r--.  1 root root  129 Dec 29  2013 .tcshrc
  ```

- **$**

  - 说明这是一个变量
  - $PATH Linux的环境变量

  ```shell
  [root@basenode /]# name=hud
  [root@basenode /]# echo name
  name
  [root@basenode /]# echo $name
  hud
  ```

- ***星号**

  - 通配符

- **~**

  - 当前用户的家目录
  - 每个用户的家目录是不同的
  - root用户家目录在系统根目录下
  - 其他用户的家目录在/home/用户名为家目录

- **空格**

  - Linux的命令与参数用空格隔开

- **/**

  - 整个Linux的文件根目录
  - 命令的参数
  - **如果是单词 一般加--**
  - **如果是字母或者缩写 一般加 -**

## **4. Linux**的文件系统

### **4.1.** **万事万物皆文件**

- 文件系统：

  - 操作系统如何管理文件，内部定义了一些规则或者定义

- 所以在Linux中所有的东西都是以文件的方式进行操作

- 在Linux中，文件的访问不和Window的一样。window依靠的是通过盘符进行访问

- Linux维护着一个树状结构的文件模型

  - 只有一个根节点 ,他的名字叫做 /
  - 一个节点上可以有多个子节点

- 查找文件的方式

  - 相对路径

    - 以当前路径为基准点，查找其他资源

    - ```sehll
      vi ../etc/sysconfig/network
      ```

  - 绝对路径

    - 以根目录为基准点，查找其他资源

    - ```shell
      vi /etc/sysconfig/network-scripts/ifcfg-ens33
      ```

    - 日常使用中，只要找到路径即可，但是如果是一些配置文件，尽量写绝对路径

- Linux查看系统进程

  ```shell
  [root@basenode ~]# ps -ef
  UID         PID   PPID  C STIME TTY          TIME CMD
  root          1      0  0 18:01 ?        00:00:01 /usr/lib/systemd/systemd --switched-root --system --deser
  root          2      0  0 18:01 ?        00:00:00 [kthreadd]
  root          4      2  0 18:01 ?        00:00:00 [kworker/0:0H]
  root          6      2  0 18:01 ?        00:00:00 [ksoftirqd/0]
  ...
  root       1496   1494  0 18:01 pts/0    00:00:00 -bash
  root       1497      2  0 18:01 ?        00:00:00 [kworker/3:1H]
  root       1512      2  0 18:01 ?        00:00:00 [kworker/1:1H]
  root       1514      2  0 18:01 ?        00:00:00 [kworker/4:1H]
  root       1518      2  0 18:06 ?        00:00:00 [kworker/4:1]
  root       1522      2  0 18:16 ?        00:00:00 [kworker/4:2]
  root       1523      2  0 18:17 ?        00:00:00 [kworker/0:1H]
  root       1524      2  0 18:21 ?        00:00:00 [kworker/1:0]
  root       1525      2  0 18:26 ?        00:00:00 [kworker/1:1]
  root       1526      2  0 18:32 ?        00:00:00 [kworker/4:0]
  root       1528   1496  0 18:33 pts/0    00:00:00 ps -ef
  
  #查看当前进程编号
  [root@basenode ~]# echo $$
  1496
  #是root       1496   1494  0 18:01 pts/0    00:00:00 -bash
  ```



### **4.2. Linux二级文件目录**

```shell
[root@basenode ~]# ll /
total 16
lrwxrwxrwx.   1 root root    7 Aug 23 00:38 bin -> usr/bin
dr-xr-xr-x.   5 root root 4096 Aug 23 00:42 boot
drwxr-xr-x   20 root root 3220 Aug 23 18:01 dev
drwxr-xr-x.  75 root root 8192 Aug 23 18:01 etc
drwxr-xr-x.   2 root root    6 Apr 11  2018 home
lrwxrwxrwx.   1 root root    7 Aug 23 00:38 lib -> usr/lib
lrwxrwxrwx.   1 root root    9 Aug 23 00:38 lib64 -> usr/lib64
drwxr-xr-x.   2 root root    6 Apr 11  2018 media
drwxr-xr-x.   2 root root    6 Apr 11  2018 mnt
drwxr-xr-x.   2 root root    6 Apr 11  2018 opt
dr-xr-xr-x  158 root root    0 Aug 23 18:01 proc
dr-xr-x---.   2 root root  135 Aug 23 01:08 root
drwxr-xr-x   23 root root  640 Aug 23 18:01 run
lrwxrwxrwx.   1 root root    8 Aug 23 00:38 sbin -> usr/sbin
drwxr-xr-x.   2 root root    6 Apr 11  2018 srv
dr-xr-xr-x   13 root root    0 Aug 23 18:01 sys
drwxrwxrwt.  11 root root  268 Aug 23 18:01 tmp
drwxr-xr-x.  13 root root  155 Aug 23 00:38 usr
drwxr-xr-x.  19 root root  267 Aug 23 00:42 var
```

> **/bin：** 
>
> bin是Binary的缩写, 这个目录存放着最经常使用的命令。 
>
> **/boot：** 
>
> 这里存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件。 
>
> **/dev ：** 
>
> dev是Device(设备)的缩写, 该目录下存放的是Linux的外部设备，在Linux中访问设备的方式和访问 
>
> 文件的方式是相同的。/etc： 
>
> 这个目录用来存放所有的系统管理所需要的配置文件和子目录。 
>
> **/home：** 
>
> 用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。 
>
> **/lib：** 
>
> 这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用 
>
> 程序都需要用到这些共享库。 
>
> **/lost+found：** 
>
> 这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。 
>
> **/media：** 
>
> linux 系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目 
>
> 录下。 
>
> **/mnt：** 
>
> 系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目 
>
> 录就可以查看光驱里的内容了。 
>
> **/opt：** 
>
> 这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认 
>
> 是空的。 
>
> **/proc：** 
>
> 这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。 
>
> 这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件， 
>
> 比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器： 
>
> echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all 
>
> **/root：** 
>
> 该目录为系统管理员，也称作超级权限者的用户主目录。 
>
> **/sbin：** 
>
> s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。 
>
> **/selinux**： 
>
> 这个目录是Redhat/CentOS所特有的目录，Selinux是一个安全机制，类似于windows的防火墙，但 
>
> 是这套机制比较复杂，这个目录就是存放selinux相关的文件的。 
>
> **/srv：** 
>
> 该目录存放一些服务启动之后需要提取的数据。 
>
> **/sys：** 
>
> 这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs 。 
>
> sysfs文件系统集成了下面3种文件系统的信息：针对进程信息的proc文件系统、针对设备的devfs文件 
>
> 系统以及针对伪终端的devpts文件系统。该文件系统是内核设备树的一个直观反映。 
>
> 当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。 
>
> **/tmp：** 
>
> 这个目录是用来存放一些临时文件的。 
>
> **/usr：** 
>
> 这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于windows下的 
>
> program files目录。 
>
> **/usr/bin：**
>
> 超级用户使用的比较高级的管理程序和系统守护程序。 
>
> **/usr/src：** 
>
> 内核源代码默认的放置目录。 
>
> **/var：** 
>
> 这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日 
>
> 志文件。 
>
> **/run：** 
>
> 是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。 
>
> 如果你的系统上有 /var/run 目录，应该让它指向 run。

### **4.3. Linux的文件操作**

- **`cd`**

  - 改变当前工作目录

- **`ls/ll`**

  - 显示出指定目录下所有的文件
  - 文件的类型
    - -普通文件
    - d文件夹
    - l软连接(类似win的快捷方式)
  - -rw-r--r--. 1 root root 3384 Nov 11 23:51 install.log.syslog

- **`mkdir`**

  - 创建文件目录

  - `mkdir -p a/b/c/d/e/f 会自动创建文件父目录`

    ```shell
    [root@basenode ~] mkdir -p a/b/c/d/e
    [root@basenode ~] cd a/b/c/d/e
    [root@basenode e] pwd
    /root/a/b/c/d/e
    ```

  - mkdir -p lucky/{1234}ls 一次可以创建多个子目录

  - **一次创建多个子目录实例**

    ```shell
    [root@basenode e]# mkdir -p shiren/{libai,baijuyi,liqingzhao}
    [root@basenode e]# ll
    total 0
    drwxr-xr-x 5 root root 52 Aug 23 19:32 shiren
    [root@basenode e]# cd shiren/
    [root@basenode shiren]# ll
    total 0
    drwxr-xr-x 2 root root 6 Aug 23 19:32 baijuyi
    drwxr-xr-x 2 root root 6 Aug 23 19:32 libai
    drwxr-xr-x 2 root root 6 Aug 23 19:32 liqingzhao
    #也就是一次性在shiren这个文件夹下创建了三个文件夹
    ```

- **`rmdir/rm -rf`**

  - 删除空文件夹

    - `rmdir: failed to remove ‘a1’: Directory not empty`
    - `rmdir: failed to remove ‘baidu’: Not a directory`

  - `rmdir`可以**安全的删除文件目录**

    ```shell
    [root@basenode e]# rmdir shiren
    rmdir: failed to remove ‘shiren’: Directory not empty
    # 使用rm -rf进行删除
    [root@basenode e]# rm -rf shiren
    [root@basenode e]# ls
    [root@basenode e]# 
    ```

- **`cp`**

  - 拷贝文件或者文件目录
    - `cp` 源文件 目标目录
    
    - `cp abcd /opt`
    
    - `cp /opt/abcd ./`
    
      ```shell
      # 将文件拷贝进文件夹
      [root@basenode ~]# cp c.txt a/b/c/
      [root@basenode ~]# cd a/b/c/
      [root@basenode c]# ls
      c.txt
      # 再拷贝出来
      [root@basenode ~]# cp a/b/c/c.txt ./
      [root@basenode ~]# ls
      a  anaconda-ks.cfg  c.txt
      ```
    
  - 拷贝文件夹
    - cp -r lucky /opt
    
      ```shell
      [root@basenode ~]# mkdir d
      [root@basenode ~]# ls
      a  anaconda-ks.cfg  c.txt  d
      [root@basenode ~]# cp -r d a/b/c/    
      [root@basenode ~]# cd a/b/c/d/
      [root@basenode d]# 
      #也可以使用通配符* ，拷贝所有以XXX为前缀的文件/文件夹
      ```
    
  - 拷贝文件夹下所有的内容
    - `cp: omitting directory ‘/root/a1’`

- **`mv`**

  - 移动文件或者文件夹（类似于剪切操作）
    - `mv a1 /opt`
    
      ```shell
      [root@basenode ~]# mv a d 
      [root@basenode ~]# ls
      anaconda-ks.cfg  c.txt  d
      [root@basenode ~]# cd d/a/b/c/
      [root@basenode c]# 
      ```
    
    - **重命名操作 `rm oldname newname`**
    
      ```shell
      [root@basenode ~]# mv c.txt a.txt
      [root@basenode ~]# ls
      anaconda-ks.cfg  a.txt  d
      ```

- **`rm`**

  - 删除文件

    - rm install.log

    - rm -f install.log

      ```shell
      [root@basenode ~]# rm a.txt
      rm: remove regular empty file ‘a.txt’? n
      [root@basenode ~]# rm -f a.txt
      [root@basenode ~]# ls
      anaconda-ks.cfg  d
      ```

- **删除文件夹**

  - rm -r abcd

  - rm -rf abcd **谨慎使用，从删库到跑路**

    ```shell
    [root@basenode ~]# ls
    anaconda-ks.cfg  d
    [root@basenode ~]# rm -r d
    rm: descend into directory ‘d’? n
    [root@basenode ~]# rm -rf d
    [root@basenode ~]# cd
    [root@basenode ~]# ls
    anaconda-ks.cfg
    ```

- **`touch`**

  - 如果没有就创建一个文件

  - **如果该文件已经存在，修改文件的三个时间，将三个时间改为当前时间（Access、Modify、Change）**

    ```shell
    [root@basenode ~]# touch readme.txt
    [root@basenode ~]# ls
    anaconda-ks.cfg  readme.txt
    ```

- **`stat`**

  - 查看文件的状态

    ```shell
    [root@basenode ~]# stat readme.txt 
      File: ‘readme.txt’
      Size: 53        	Blocks: 8          IO Block: 4096   regular file
    Device: fd00h/64768d	Inode: 134340463  (硬连接数量) Links: 1
    #权限 Access: (0644/-rw-r--r--) #所属用户Uid: (    0/    root)   #所属组Gid: (    0/    root)
    Access: 2022-08-23 22:15:14.916692909 +0800
    Modify: 2022-08-23 22:15:14.916692909 +0800
    Change: 2022-08-23 22:15:14.916692909 +0800
     Birth: -
    # 使用vi 命令进行编辑后 时间变化了
    #[root@basenode ~]# stat readme.txt 
    File: ‘readme.txt’
    Size: 53        	Blocks: 8          IO Block: 4096   regular file
    Device: fd00h/64768d	Inode: 134340463   Links: 1
    Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
    Access: 2022-08-23 22:18:43.207678781 +0800
    Modify: 2022-08-23 22:15:14.916692909 +0800
    Change: 2022-08-23 22:15:14.916692909 +0800
    
    ```

  - Inode 当前文件在文件系统的唯一标识，类似于ID

  - 时间

    - access 访问时间
    - modify 修改文件内容时间
    - change 修改文件元数据信息时间
      - 文件大小 ，文件所有者 ，文件权限
      - 对于文件的描述信息

- **`ln`**

  - 创建文件的链接

  - 软(符号)连接 `-s`

    ```sh
    [root@basenode ~]# ln -s a.txt a.link 
    [root@basenode ~]# ll
    total 12
    lrwxrwxrwx  1 root root    5 Aug 23 22:52 a.link -> a.txt
    -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
    -rw-r--r--  1 root root   28 Aug 23 22:51 a.txt
    -rw-r--r--  1 root root   53 Aug 23 22:15 readme.txt
    # 看一下a.link
    [root@basenode ~]# cat a.link 
    abcdefghijklmnopqrstuvwxyz
    # 发现是a.txt里面的内容
    ```

    - 软连接和原始文件不是同一个文件
      - lucky1 131085
      - sl 131074
    - rm -rf lucky1

  - 硬链接 就是后面不带`-s`参数

    - ```sh
      [root@basenode ~]# ln  a.txt a.ylink 
      [root@basenode ~]# ls -l
      total 16
      lrwxrwxrwx  1 root root    5 Aug 23 22:52 a.link -> a.txt
      -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
      -rw-r--r--  2 root root   28 Aug 23 22:51 a.txt
      -rw-r--r--  2 root root   28 Aug 23 22:51 a.ylink
      -rw-r--r--  1 root root   53 Aug 23 22:15 readme.txt
      ```

    - 硬链接和原始文件使用文件系统中的同一个文件

    - 如果你害怕一个文件被别人误删，你可以使用硬链接保护这个文件

  - 软硬链接在链接文件的时候，推荐使用文件的绝对路径,否则有可能会出现问题、

  - 如果删除了源文件，看看会怎么样？

    ```sh
    [root@basenode ~]# ll -l
    total 12
    lrwxrwxrwx  1 root root    5 Aug 23 22:52 a.link -> a.txt
    -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
    -rw-r--r--  1 root root   28 Aug 23 22:51 a.ylink
    -rw-r--r--  1 root root   53 Aug 23 22:15 readme.txt
    ```

    a.link这个时候心态炸了，因为源文件没了，他也没有存在的意义了。

    ```sh
    #硬连接依旧
    [root@basenode ~]# cat a.ylink 
    abcdefghijklmnopqrstuvwxyz	
    ```

  - 这里来看看a.txt

    ```sh
    [root@basenode ~]# stat a.txt 
      File: ‘a.txt’
      Size: 26        	Blocks: 8          IO Block: 4096   regular file
    Device: fd00h/64768d	Inode: 134340464   Links: 2
    Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
    Access: 2022-08-23 23:07:50.962478837 +0800
    Modify: 2022-08-23 23:07:50.962478837 +0800
    Change: 2022-08-23 23:08:18.882476943 +0800
     Birth: -
    #可以看到这里links的数量是2，硬连接直接指向内存中的a.txt而软连接指向被删除的a.txt
    ```

### **4.4 ** **读取文件信息**

- **cat**
  - 将整个文档加载到内存中，并进行一次性显示
  - 除非后面使用管道，传递数据
  
- **tac**
  
  - 将整个文档加载到内存中，并进行一次性按行逆序显示
  
- **more/less**
  - 分页查看文档内容
  - 快捷键
    - 回车 下一行
    - 空格 下一页
    - b 回退
    - q 退出
  
- **head**
  - 从文章开始读取N行
  
  - 默认如果超过10行读取10行,否则读取现在行数
  
  - head -5 profile
  
    ```sh
    [root@basenode ~]# head -5 profile 
    # /etc/profile
    
    # System wide environment and startup programs, for login setup
    # Functions and aliases go in /etc/bashrc
    
    ```
  
- **tail**
  
  - 从文章末尾读取N行
  
  - head -3 profile | tail -1
  
    ```shell
    [root@basenode ~]# head -3 profile |tail -1
    # System wide environment and startup programs, for login setup
    ```
  
    - 利用管道只读取第N行管道的作用就相当于把前面的结果以参数的方式传递给后面的命令
  
  - 读取新增数据
    - ping www.baidu.com >>baidu
    
    - tail -F baidu
    
    - 如果f:
      - 它会监听指定inode的文件数据变化，但是当文件被删除后
      
      - 即使创新创建，inode也会发生变化，于是监听失败
      
        ```sh
        [root@basenode ~]# tail -f aliyun
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=3 ttl=128 time=38.3 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=4 ttl=128 time=39.6 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=5 ttl=128 time=37.8 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=6 ttl=128 time=38.4 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=7 ttl=128 time=39.5 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=8 ttl=128 time=38.9 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=9 ttl=128 time=38.8 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=10 ttl=128 time=39.8 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=11 ttl=128 time=37.9 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=12 ttl=128 time=38.6 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=13 ttl=128 time=39.7 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=14 ttl=128 time=38.0 ms
        64 bytes from 203.119.207.114 (203.119.207.114): icmp_seq=15 ttl=128 time=40.3 ms
        ```
      
    - 如果F
      - 他会监听指定名字的文件,如果文件被删除后，重新创建
      - 他会重新监听新文件的数据变化，监听不受影响
      - **-F代表可以在同名文件中继续进行监听**
    
  - #### -f监听的INode，-F监听的是名字
  
- **find**
  
  - 查找指定的文件
  
  - find 要查找的范围 -name 名字
  
    ```sh
    # 例如要进行全局搜索a.txt
    [root@basenode ~]# find / -name readme.txt
    /root/readme.txt
    /root/a/b/c/readme.txt
    #找到在两个地方有这个文件
    ```
  
  - find /etc -name profile
  
    ```sh
    [root@basenode ~]# find /etc -name profile
    /etc/lvm/profile
    /etc/profile
    ```
  
  - 使用通配符進行查询的时候
  
    ```sh
    [root@basenode ~]# find / -name r*
    /root/readme.txt
    /root/a/b/c/readme.txt
    ```



### 4.5. VI和VIM编辑器

![](C:\Users\Hud\Desktop\文件（需要）\截图\vim.png)

#### 4.5.1 打开文件

- **正常打开**
  - vi profile
- **打开文件，并将光标置于第8行**
  - vi +8 profile
- **打开最后一行**
  - vi + profile
- **打开指定搜索单词的位置**
  - vi +/if profile
  - 按n查找下一个，按N查找上一个



#### **4.5.2 **三种模式

- 编辑模式
  - 编辑模式中，每一个按键都有其他的功能
- 输入模式
  - 每一个按键按下什么，就像文本中数据输入什么
- 末行（命令行）模式
  - 我们可以直接在VI中输入特定的命令



#### 4.5.3 三种模式的切换

![](C:\Users\Hud\Desktop\文件（需要）\截图\vi模式切换.png)

- **vi 命令默认进入编辑模式**（每个按键都有特殊含义）
- 编辑模式-->输入模式
  - i在当前位置插入数据
  - a追加数据
  - o在当前行后面开启一个新的输入行
  - I 行首
  - A 行尾
  - O 上一行
- 输入模式-->编辑模式
  - 按下`ESC`
- 编辑模式-->末行模式
  - :
  - 末行模式-->编辑模式
  - 按下`ESC`

#### **4.5.4.** **编辑模式**

- G最后一行
- gg 跳转到第一行
- 数字gg 跳转到第数字行（15 gg）
- w 下个单词
- 数字w
- dw 删除一个单词
- 3dw 删除三个单词
- dd 删除一行
- 3dd 删除三行
- u回退到前面的操作
- .回退u执行的操作
- yw 复制一个单词
- 3yw 复制三个单词
- yy 复制一行
- 3yy复制三行
- p粘贴
- 6p 粘贴6次
- x 剪切
- 3x 剪切三个字符r 替换，然后输入一个字符替换
- 3r 替换三个
- hjkl 方向键
- ZZ 保存并退出
- ctrl+s 锁屏 ctrl+q 解锁



#### **4.5.5.** **输入模式**

没得讲。按啥是啥



#### **4.5.6.** **末行模式**

- `set nu` 设置行号

- `set nonu` 取消行号

- `w` 保存

- `q` 退出

- `wq` 保存并退出

- `q!`强制退出，但是不保存

- 如果上次异常退出会保留同名隐藏文件，每次启动会给与提示

  - 如果确定当前文件没问题，请删除隐藏文件

- `/pattern`

  - 搜索指定的字符串

  - ```sh
    /if
    ```

- /usr n向下查找 N逆向查找

- s/p1/p2/g

- 替换字符串

- g 替换当前行所有 否则只替换当前行第一个

- ```sh
  s/hud/monica/g
  ```

- 查找指定行

- 3,8s/abc/lucky/g

- 替换全文

- ```
  g/abc/s//lucky/g
  ```

  ![](C:\Users\Hud\Desktop\文件（需要）\截图\vim键.png)

  

### **4.6.** **计算机间的数据传输**

#### **4.6.1. Window--Linux**

- **lrzsz**
  - 需要手动安装
    - yum install lrzsz -y
  - **rz**
    - 将文件从window上传到Linux
  - **sz** 
    - 将文件从Linux传输到Window
- **xftp**
  - 较为通用的文件传输方式

**如果现在没有xftp，那么你就使用lrzsz**

- **安装lrzsz**

  ```shell
  [root@basenode ~]# yum install lrzsz -y
  Loaded plugins: fastestmirror
  Loading mirror speeds from cached hostfile
  ...
  Complete!
  ```

- **输入rz指令，并且选中指定的文件进行上传**

  ```sh
  [root@basenode ~]# rz
  
  [root@basenode ~]# ll
  total 212
  -rw-r--r--  1 root root 169209 Aug 25 06:53 aliyun
  -rw-------. 1 root root   1537 Aug 23 00:41 anaconda-ks.cfg
  -rw-r--r--  1 root root     53 Aug 25 22:20 a.txt
  -rw-r--r--  1 root root     62 Aug 25 15:38 from_Win.txt
  -rw-r--r--  1 root root   1819 Aug 25 19:03 profile
  -rw-r--r--  1 root root     64 Aug 25 21:42 readme.txt
  [root@basenode ~]# cat from_Win.txt 
  This is from Hud's Win11 to say 'Hello'!
  Have a good day~ ^.^
  [root@basenode ~]# 
  ```

- **输入`sz xxx文件`指令，将xxx文件发送至Win**

  ```sh
  [root@basenode1 ~]# sz from_Linux.txt
  ```

#### **4.6.2. Linux--Linux**

- `scp` 源数据地址(source) 目标数据地址(target)

  ```sh
  [root@basenode1 ~]# scp basenode1 root@192.168.88.111:~/FfromB1 
  root@192.168.88.111's password: 
  basenode1                                                                           100%   32    34.0KB/s   00:00 
  ```

  看看`basenode2`，有没有成功：

  ```
  [root@basenode2 FfromB1]# ls
  basenode1
  ```

  **文件成功传输！**

- 如果想在`basenode2`上面将`basende1`的内容给拿过来，也是可以的 

  ```sh
  [root@basenode2 ~]# scp root@192.168.88.110:~/readme.txt ./
  root@192.168.88.110's password: 
  readme.txt                                                                          100%   64    50.0KB/s   00:00    
  [root@basenode2 ~]# ll
  total 8
  -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
  drwxr-xr-x  2 root root   23 Aug 26 00:48 FfromB1
  -rw-r--r--  1 root root   64 Aug 26 00:53 readme.txt
  ```

- 如果要拷貝文件夾，加上**-r**

  ```sh
  [root@basenode2 ~]# scp -r  root@192.168.88.110:~/base1 ./FfromB1/
  root@192.168.88.110's password: 
  [root@basenode2 ~]# ls FfromB1/
  base1  basenode1
  ```

  

### **4.7.** **文件大小**

- **分区信息**

  - **df 查看分区信息**

    ```sh
    [root@basenode1 ~]# df cha
    Filesystem              1K-blocks    Used Available Use% Mounted on
    devtmpfs                  1918640       0   1918640   0% /dev
    tmpfs                     1930644       0   1930644   0% /dev/shm
    tmpfs                     1930644   11816   1918828   1% /run
    tmpfs                     1930644       0   1930644   0% /sys/fs/cgroup
    /dev/mapper/centos-root 125501572 1448556 124053016   2% /
    /dev/sda1                  258724  134028    124696  52% /boot
    tmpfs                      386132       0    386132   0% /run/user/0
    ```

  - **df -h**

    ```sh
    [root@basenode1 ~]# df -h
    Filesystem               Size  Used Avail Use% Mounted on
    devtmpfs                 1.9G     0  1.9G   0% /dev
    tmpfs                    1.9G     0  1.9G   0% /dev/shm
    tmpfs                    1.9G   12M  1.9G   1% /run
    tmpfs                    1.9G     0  1.9G   0% /sys/fs/cgroup
    /dev/mapper/centos-root  120G  1.4G  119G   2% /
    /dev/sda1                253M  131M  122M  52% /boot
    tmpfs                    378M     0  378M   0% /run/user/0
    ```

- **指定文件目录大小**

  - **du -h --max-depth=1 文件（--max-depth=1表示最大深度）**

    ```sh
    [root@basenode2 ~]# du -h --max-depth=1  FfromB1/
    0	FfromB1/base1
    4.0K	FfromB1/
    #你看 这里就不会显示再下级目录的大小了
    ```

- **swap**

  - 一个特殊分区，以硬盘代替内存当内存使用满的时候，可以将一部分数据写出到swap分区
  - 当内存使用满的时候，可以将一部分数据写出到swap分区



### **4.8.** **文件压缩**

#### **4.8.1. tar**

- 主要针对的文件是`xxx.tar.gz`

- 解压缩

  - tar -zx(解压)v(过程)f(文件) lucky.tar.gz

- 压缩

  - tar -zc(压缩)f(文件)  xxx.tar.gz(压缩后的名字)   xxx(源文件)

    ```sh
    # 压缩文件readme.txt
    [root@basenode1 ~]# tar -zcf readme.tar.gz readme.txt
    [root@basenode1 ~]# ll
    total 16
    -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
    drwxr-xr-x  3 root root   16 Aug 26 00:23 base1
    -rw-r--r--  1 root root   32 Aug 26 00:40 basenode1
    -rw-r--r--  1 root root  173 Aug 26 18:16 readme.tar.gz
    -rw-r--r--  1 root root   64 Aug 25 21:42 readme.txt
    ```

  - tar -zxf xxx.tar.gz -C /opt/

    - -C 指定解压缩的文件目录

      ```sh
      [root@basenode1 ~]# tar -zxvf readme.tar.gz -C base1 
      readme.txt
      [root@basenode1 ~]# cd base1
      [root@basenode1 base1]# ll
      total 4
      -rw-r--r-- 1 root root 64 Aug 25 21:42 readme.txt
      [root@basenode1 base1]# cat readme.txt 
      this is hud learning Linux!
      Be better and stronger!
      a new line!
      ```

#### **4.8.2. zip和unzip**

- 安装

  - ```shell
    yum install zip unzip -y
    ```

- 压缩

  - `zip -r xxx.zip xxx`

    ```sh
    [root@basenode1 ~]# 
    [root@basenode1 ~]# zip -r base1.zip base1
      adding: base1/ (stored 0%)
      adding: base1/readme.txt (deflated 5%)
    [root@basenode1 ~]# ll
    total 12
    -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
    drwxr-xr-x  2 root root   24 Aug 26 18:52 base1
    -rw-r--r--  1 root root  383 Aug 26 18:54 base1.zip
    -rw-r--r--  1 root root   32 Aug 26 00:40 basenode1
    ```

- 解压缩

  - unzip xxx.zip

    ```sh
    # 先看看base1文件夹
    [root@basenode1 ~]# ll ~/base1
    total 0
    # 解压文件base1.zip(里面有一个readme.txt)
    [root@basenode1 ~]# unzip  base1.zip 
    Archive:  base1.zip
      inflating: base1/readme.txt        
    [root@basenode1 ~]# ll ~/base1
    total 4
    -rw-r--r-- 1 root root 64 Aug 25 21:42 readme.txt
    ```



## **5. Linux**的网络信息

### **5.1** **主机名称**

- 临时修改

  ```sh
  hostname xxx
  ```

- 长久修改

  ```sh
  vi /etc/hostname
  ```

### **5.2. DNS**解析

- 域名解析服务

- 可以将域名转换为IP地址

- DNS域名劫持

  - window --> C:\Windows\System32\drivers\etc\hosts
  - 123.56.138.186 www.baidu.com
  - 123.56.138.186 www.taodao.com

- 修改主机域名

- vi /etc/hosts

  ```sh
  # 这个是环网地址
  127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
  #ip6
  ::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
  ```

- 将来我们需要把所有的虚拟机都配置hosts文件

  ```sh
  192.168.88.110 node01
  192.168.88.111 node02
  ```

  

### **5.3.** **网络相关命令**

- **ifconfig**

  - 查看当前网卡的配置信息

  - 这个命令属于 net-tools中的一个命令，但是Centos7中minimal版并没有集成这个包

  - 所以7的时候需要自己手动安装

  - 如果没有ifconfig ，可以使用ip addr 临时代替

    ```sh
    [root@tempnode ~]# ifconfig
    ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.88.110  netmask 255.255.255.0  broadcast 192.168.88.255
            inet6 fe80::8c49:66e4:381a:f151  prefixlen 64  scopeid 0x20<link>
            ether 00:0c:29:b3:09:d0  txqueuelen 1000  (Ethernet)
            RX packets 4033  bytes 1076275 (1.0 MiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 2454  bytes 298291 (291.2 KiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    
    lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 1000  (Local Loopback)
            RX packets 10  bytes 840 (840.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 10  bytes 840 (840.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ```

- netstat

  - 查看当前网络的状态信息
  - 一个机器默认有65536个端口号[0,65535]
  - 这是一个逻辑的概念，将来我们需要使用程序监听指定的端口，等待别人的访问
  - 一个端口只能被一个程序所监听, 端口已经被占用

- netstat -anp

  ```sh
  [root@tempnode ~]# netstat -anp
  Active Internet connections (servers and established)
  Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
  tcp        0      0 0.0.0.0:22(默认的ssh)    0.0.0.0:*               LISTEN      1017/sshd           
  tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1221/master         
  tcp        0      0 192.168.88.110:22       192.168.88.1:52839      ESTABLISHED 1497/sshd: root@pts 
  tcp        0      0 192.168.88.110:22       192.168.88.1:57861      ESTABLISHED 1892/sshd: root@pts 
  tcp        0      0 192.168.88.110:22       192.168.88.1:57957      ESTABLISHED 1910/sshd: root@pts 
  tcp6       0      0 :::22#(ip4的ssh)        :::*                    LISTEN      1017/sshd           
  tcp6       0      0 ::1:25                  :::*                    LISTEN      1221/master         
  raw6       0      0 :::58                   :::*                    7           764/NetworkManager  
  Active UNIX domain sockets (servers and established)
  ...
  ```

  可以看到某些端口正在被监听

- **netstat -r 核心路由表 == route**

  ```sh
  Kernel IP routing table
  Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
  default         gateway         0.0.0.0         UG        0 0          0 ens33
  192.168.88.0    0.0.0.0         255.255.255.0   U         0 0          0 ens33
  ```

- ping

  - 查看与目标IP地址是否能够连通（**但是端口不能**）

- telnet

  - 查看与目标IP的指定端口是否能够连通

  - yum install telnet -y

  - ```sh
    [root@tempnode ~]# telnet node02 22
    Trying 192.168.88.111...
    Connected to node02.
    Escape character is '^]'.
    SSH-2.0-OpenSSH_7.4
    ```

- curl

  - restful 我们所有的资源在网络上中都有唯一的定位

  - 那么我们可以通过这个唯一定位标识指定的资源

  - http://localhost:8080/lucky/user.action/666

  - curl -X GET http://www.baidu.com // 获取对应网站资源

    ```sh
    [root@tempnode ~]# curl -X GET http://www.baidu.com >>baidu 
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
    100  2381  100  2381    0     0  49668      0 --:--:-- --:--:-- --:--:-- 50659
    [root@tempnode ~]# cat baidu 
    <!DOCTYPE html>
    <!--STATUS OK--><html> <head><meta http-equiv=content-type content=text/html;charset=utf-8><meta http-equiv=X-UA-Compatible content=IE=Edge><meta content=always name=referrer><link rel=stylesheet type=text/css href=http://s1.bdstatic.com/r/www/cache/bdorz/baidu.min.css><title>百度一下，你就知道</title></head> <body link=#0000cc> <div id=wrapper> <div id=head> <div class=head_wrapper> <div class=s_form> <div class=s_form_wrapper> <div id=lg> <img hidefocus=true src=//www.baidu.com/img/bd_logo1.png width=270 height=129> </div> <form id=form name=f action=//www.baidu.com/s class=fm> <input type=hidden name=bdorz_come value=1> <input type=hidden name=ie value=utf-8> <input type=hidden name=f value=8> <input type=hidden name=rsv_bp value=1> <input type=hidden name=rsv_idx value=1> <input type=hidden name=tn value=baidu><span class="bg s_ipt_wr"><input id=kw name=wd class=s_ipt value maxlength=255 autocomplete=off autofocus></span><span class="bg s_btn_wr"><input type=submit id=su value=百度一下 class="bg s_btn"></span> </form> </div> </div> <div id=u1> <a href=http://news.baidu.com name=tj_trnews class=mnav>新闻</a> <a href=http://www.hao123.com name=tj_trhao123 class=mnav>hao123</a> <a href=http://map.baidu.com name=tj_trmap class=mnav>地图</a> <a href=http://v.baidu.com name=tj_trvideo class=mnav>视频</a> <a href=http://tieba.baidu.com name=tj_trtieba class=mnav>贴吧</a> <noscript> <a href=http://www.baidu.com/bdorz/login.gif?login&amp;tpl=mn&amp;u=http%3A%2F%2Fwww.baidu.com%2f%3fbdorz_come%3d1 name=tj_login class=lb>登录</a> </noscript> <script>document.write('<a href="http://www.baidu.com/bdorz/login.gif?login&tpl=mn&u='+ encodeURIComponent(window.location.href+ (window.location.search === "" ? "?" : "&")+ "bdorz_come=1")+ '" name="tj_login" class="lb">登录</a>');</script> <a href=//www.baidu.com/more/ name=tj_briicon class=bri style="display: block;">更多产品</a> </div> </div> </div> <div id=ftCon> <div id=ftConw> <p id=lh> <a href=http://home.baidu.com>关于百度</a> <a href=http://ir.baidu.com>About Baidu</a> </p> <p id=cp>&copy;2017&nbsp;Baidu&nbsp;<a href=http://www.baidu.com/duty/>使用百度前必读</a>&nbsp; <a href=http://jianyi.baidu.com/ class=cp-feedback>意见反馈</a>&nbsp;京ICP证030173号&nbsp; <img src=//www.baidu.com/img/gs.gif> </p> </div> </div> </div> </body> </html>
    
    ```

### **5.4** 防火墙

- 防火墙技术是通过有机结合各类用于安全管理与筛选的软件和硬件设备，帮助计算机网络于其内、外网之间构建一道相对隔绝的保护屏障，以保护用户资料与信息安全性的一种技术

- 在CentOS 7+中 使用firewalld代替以前的 iptables 

  - **查看防火墙的状态**

  ```sh
  systemctl status firewalld.service
  [root@tempnode ~]# systemctl status firewalld.service
  firewalld.service - firewalld - dynamic firewall daemon
     Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
     Active: inactive (dead)
       Docs: man:firewalld(1)
  ```

  - **临时停止firewall** 

    ```sh
    systemctl stop firewalld.service 
    ```

  - **禁止firewall开机启动** 

    ```sh
    systemctl disable firewalld.service 
    ```

  - ```sh
    firewall-cmd --state		 		##查看防火墙状态，是否是running 
    firewall-cmd --reload 				##重新载入配置，比如添加规则之后，需要执行此命令 
    firewall-cmd --get-zones 			##列出支持的zone 
    firewall-cmd --get-services 		##列出支持的服务，在列表中的服务是放行的 
    firewall-cmd --query-service ftp 	##查看ftp服务是否支持，返回 yes或者no 
    firewall-cmd --add-service=ftp 		##临时开放ftp服务 
    firewall-cmd --add-service=ftp --permanent ##永久开放ftp服务 
    firewall-cmd --remove-service=ftp --permanent ##永久移除ftp服务
    firewall-cmd --add-port=80/tcp --permanent 	  ##永久添加80端口
    ```

- 开启一个端口的正确操作

  ```sh
  # 添加 
  firewall-cmd --zone=public --add-port=80/tcp --permanent 
  
  #重新载入
  firewall-cmd --reload
  
  #查看 
  firewall-cmd --zone=public --query-port=80/tcp 
  
  #删除 
  firewall-cmd --zone=public --remove-port=80/tcp --permanent
  ```

  **实例**

  ```sh
  [root@tempnode ~]# systemctl start firewalld.service
  [root@tempnode ~]# firewall-cmd --zone=public --add-port=80/tcp --permanent 
  success
  [root@tempnode ~]# firewall-cmd --reload
  success
  [root@tempnode ~]# firewall-cmd --zone=public --query-port=80/tcp 
  yes
  [root@tempnode ~]# firewall-cmd --zone=public --remove-port=80/tcp --permanent
  success
  ```

  

### **5.5.** **加密算法**

#### **5.5.1.** **不可逆加密算法**

**举个例子(7+8=15,15=?+?)**

- **可以通过数据计算加密后的结果，但是通过结果无法计算出加密数据**
- 应用场景
  - Hash算法常用在不可还原的密码存储、信息完整性校验。
  - 文档、音视频文件、软件安装包等用新老摘要对比是否一样(接收到的文件是否被修改)
  - 用户名或者密码加密后数据库存储(数据库大多数不会存储关键信息的明文，就像很多登录功
- 能的忘记密码不能找回，只能重置)
- 案例
- 123456
- e10adc3949ba59abbe56e057f20f883e
- **md5**(md5(123456))-----**md5**(654321)



#### **5.5.2.** **对称加密算法**

![image-20220826195249404](C:\Users\Hud\AppData\Roaming\Typora\typora-user-images\image-20220826195249404.png)

- Symmetric Key Encryption
- 代表性算法叫做 DES、3DES、Blowfish、IDEA、RC4、RC5、RC6和AES
- 特点
  - 加密和解密使用相同的秘钥
- 优点
  - 生成密钥的算法公开、计算量小、加密速度快、加密效率高、密钥较短
- 缺点
  - 双方共同的密钥，有一方密钥被窃取，双方都影响
  - 如果为每个客户都生成不同密钥，则密钥数量巨大，密钥管理有压力
- 应用场景
  - 登录信息用户名和密码加密、传输加密、指令加密
- 案例:
  - 原文：今晚八点学校小树林见
  - 密钥： love
  - 7gjM6FhIc89ACoel+jJ3VM26XGAdSlaHTj5NYg4VkKA=



#### **5.5.3.** **非对称加密算法**

![image-20220826200724922](C:\Users\Hud\AppData\Roaming\Typora\typora-user-images\image-20220826200724922.png)

- Asymmetric Key Encryption
- 非对称加密算法需要一对密钥(两个密钥)：
  - 公开密钥(publickey)和私有密钥(privatekey)(简称公钥，私钥)。
  - 公开密钥与私有密钥生成时是一对
  - 用公钥加密只能是对应的私钥解密，同理用私钥加密只能用对应的公钥解密。
- 代表性算法叫做 RSA、ECC、Diffie-Hellman、El Gamal、DSA(数字签名用)
- 优点：
  - 安全高(几乎很难破解)
- 缺点
  - 加解密相对速度慢、密钥长、计算量大、效率低
- 应用场景
  - HTTPS(ssl)证书里制作、CRS请求证书、金融通信加密、蓝牙等硬件信息加密配对传输、关键的登录信息验证。
- http://tool.chacuo.net/cryptrsaprikey



### **5.6.** **主机间的相互免秘钥**

- 可以通过ssh命令免秘钥连接到其他的主机

  ```sh
  [root@basenode1 ~]# ssh 192.168.88.111
  root@192.168.88.111's password: 
  Last login: Sat Aug 27 03:34:23 2022 from 192.168.88.1
  ```

- 如果是第一次建立连接，需要输入yes

  - 在 ~/.ssh/known_hosts 文件记录了以前访问地址(ip hostname)的信息
  - 在访问地址的时候如果没有收录到known_hosts文件中，就需要输入yes
  - 如果以前收录到known_hosts中，直接输入密码即可

- 需要输入密码

  - **生成秘钥(生成公钥和私钥再将公钥发送给别人)**

    - ```sh
      ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa		# 加密方式rsa -P密码为空 默认存放在~/.ssh/id_rsa位置
      ```

      ```sh
      [root@basenode1 ~]# ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
      Generating public/private rsa key pair.
      Your identification has been saved in /root/.ssh/id_rsa.   #私钥
      Your public key has been saved in /root/.ssh/id_rsa.pub.   #公钥
      The key fingerprint is:
      SHA256:jcVBGurL36B9bAhrEpbXqjupcb+NegRO1exvT3XaEN8 root@basenode1
      The key's randomart image is:
      +---[RSA 2048]----+
      |       o..o      |
      |      ..o+ .  .  |
      |     .... o    o.|
      |    o.  .+    o E|
      |   o o..S..  . = |
      |    =.+.. o . . .|
      |  ...=o+.+ o     |
      |   o+.=*.o+ .    |
      |  ..+O=.+o.      |
      +----[SHA256]-----+
      ```

  - **如果你想免秘钥登录谁，只需要把自己的公钥传递给对方主机即可**

    **这个秘钥要放在 ~/.ssh/authorized_keys**

    ```sh
    [root@basenode1 ~]# ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.88.111
    /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
    /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
    /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
    root@192.168.88.111's password: 
    
    Number of key(s) added: 1
    
    Now try logging into the machine, with:   "ssh 'root@192.168.88.111'"
    and check to make sure that only the key(s) you wanted were added.
    ```

    - 在node2中查看

    ```sh
    [root@basenode2 .ssh]# cat authorized_keys 
    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDkwI/IRw2lYHPaNsEXvvlmI0TNr+PMIiXY77WLnuimmyinXJK6qn8FYBkHtsjBrzu4P8a6Zhg/VoKFxUKPcQzMQS2RqAOkOL0lcjTkfganhCMiaj84KZXW4/ZFAlh1ZNZ0SdFHU5TlyXrDdcn8ozktE1soJ8kgnQjYWvhcJ/gUqVnlImRLxkEPtDli2xTaDLwxpcGWDF+Ou4LdRRaxwVaHULidi4xgCuHXXJLkdiXvR5ifTZW//J+O1BUL3jw5PbBNJf9CcgjAVibBWhsU5rmYcuyf7VFg0K18iEbXYa21Obye03ncmaDt0DnobiSDMsJfW9u6rzovocnab9Q2rpvn root@basenode1
    ```

  - **这个时候就可以免密钥登录了**

    ```sh
    [root@basenode1 ~]# ssh node02
    Last login: Sat Aug 27 04:01:22 2022 from node01
    [root@basenode2 ~]# 
    ```

    ![image-20220826225147202](C:\Users\Hud\AppData\Roaming\Typora\typora-user-images\image-20220826225147202.png)

    ​																										

```sh
[root@basenode1 ~]# vi ~/.ssh/known_hosts 
192.168.88.111 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNWh+/Z9Lxr0he6B+4YubSh+jnDCrFneRqeqQCVX5eb3vFOCgP9gl+wxWIz2pQACgQOW0BZV7+kJTl2MQ6dXL1I=
node02 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNWh+/Z9Lxr0he6B+4YubSh+jnDCrFneRqeqQCVX5eb3vFOCgP9gl+wxWIz2pQACgQOW0BZV7+kJTl2MQ6dXL1I=
localhost ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNWh+/Z9Lxr0he6B+4YubSh+jnDCrFneRqeqQCVX5eb3vFOCgP9gl+wxWIz2pQACgQOW0BZV7+kJTl2MQ6dXL1I=
```

- 如果我把这个文件的内容全部都删除，那么下次连通的时候，就会需要yes。。。

  ```sh
  [root@basenode1 ~]# ssh node02
  The authenticity of host 'node02 (192.168.88.111)' can't be established.
  ECDSA key fingerprint is SHA256:brYl4mGgxLJPUJ2atn8FUM+Mur86T+z8QliExT51JZs.
  ECDSA key fingerprint is MD5:ec:fe:75:03:ca:d6:5c:71:30:3f:f9:3f:58:1c:84:94.
  Are you sure you want to continue connecting (yes/no)? yes
  Warning: Permanently added 'node02' (ECDSA) to the list of known hosts.
  Last login: Sat Aug 27 04:02:47 2022 from 192.168.88.1
  [root@basenode2 ~]# 
  ```

- 现在再回到node01 ，把~/.ssh/known_hosts中的node02删了

  怎么办呢？ 看看下面

### **5.7.** **主机名与Host校验**

- 错误原因:

  - **Cannot determine realm for numeric host**

- 解决方案1--本次

  - ```sh
    ssh -v -o GSSAPIAuthentication=no root@node02		#亲测好像无效
    ```

- 解决方案2--所有

  - 修改/etc/ssh/ssh_config文件的配置，以后则不会再出现此问题

  - 最后面添加：

    - ```sh
      StrictHostKeyChecking no
      
      UserKnownHostsFile /dev/null
      ```

  - **这样就行了，不检查了**

    ```sh
    [root@basenode1 ~]# vi /etc/ssh/ssh_config
    [root@basenode1 ~]# ssh node02
    Warning: Permanently added 'node02,192.168.88.111' (ECDSA) to the list of known hosts.
    Last login: Sat Aug 27 04:37:24 2022 from node01
    [root@basenode2 ~]# 
    ```




## **6.** **日期与时间**

### **6.1.** **时间命令**

- **查看时区**

  - `ll /etc/localtime`

  ```sh
  [root@basenode1 ~]# ll /etc/localtime 
  lrwxrwxrwx. 1 root root 35 Aug 23 00:41 /etc/localtime -> ../usr/share/zoneinfo/Asia/Shanghai
  ```

- **cal 查看日历**

  ```sh
  [root@basenode1 ~]# cal 2022
                                 2022                               
  
         January               February                 March       
  Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa
                     1          1  2  3  4  5          1  2  3  4  5
   2  3  4  5  6  7  8    6  7  8  9 10 11 12    6  7  8  9 10 11 12
   9 10 11 12 13 14 15   13 14 15 16 17 18 19   13 14 15 16 17 18 19
  16 17 18 19 20 21 22   20 21 22 23 24 25 26   20 21 22 23 24 25 26
  23 24 25 26 27 28 29   27 28                  27 28 29 30 31
  30 31
          April                   May                   June        
  Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa
                  1  2    1  2  3  4  5  6  7             1  2  3  4
   3  4  5  6  7  8  9    8  9 10 11 12 13 14    5  6  7  8  9 10 11
  10 11 12 13 14 15 16   15 16 17 18 19 20 21   12 13 14 15 16 17 18
  17 18 19 20 21 22 23   22 23 24 25 26 27 28   19 20 21 22 23 24 25
  24 25 26 27 28 29 30   29 30 31               26 27 28 29 30
  
          July                  August                September     
  Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa
                  1  2       1  2  3  4  5  6                1  2  3
   3  4  5  6  7  8  9    7  8  9 10 11 12 13    4  5  6  7  8  9 10
  10 11 12 13 14 15 16   14 15 16 17 18 19 20   11 12 13 14 15 16 17
  17 18 19 20 21 22 23   21 22 23 24 25 26 27   18 19 20 21 22 23 24
  24 25 26 27 28 29 30   28 29 30 31            25 26 27 28 29 30
  31
         October               November               December      
  Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa
                     1          1  2  3  4  5                1  2  3
   2  3  4  5  6  7  8    6  7  8  9 10 11 12    4  5  6  7  8  9 10
   9 10 11 12 13 14 15   13 14 15 16 17 18 19   11 12 13 14 15 16 17
  16 17 18 19 20 21 22   20 21 22 23 24 25 26   18 19 20 21 22 23 24
  23 24 25 26 27 28 29   27 28 29 30            25 26 27 28 29 30 31
  30 31
  ```

- **修改时间**

  ```sh
  [root@basenode1 ~]# date -s 2022-8-27
  Sat Aug 27 00:00:00 CST 2022
  ```

- **查看时间**

  ```sh
  [root@basenode1 ~]# date
  Sat Aug 27 00:00:19 CST 2022
  ```

  **现在时间不对**



### **6.2.** **日期自动同步**

- 自动同步时间

- yum install ntp -y

- `ntpdate cn.ntp.org.cn`

  ```sh
  [root@basenode1 ~]# ntpdate cn.ntp.org.cn
  27 Aug 09:47:29 ntpdate[1999]: step time server 114.67.237.130 offset 33053.431405 sec
  [root@basenode1 ~]# data
  -bash: data: command not found
  [root@basenode1 ~]# date
  Sat Aug 27 09:47:43 CST 2022
  ```

- 本地搭建NTP服务

  - 开启本地NTP服务器

    - 在node1节点上：`service ntpd start`

  - 在node2节点上同步时间至node1

    ```sh
    [root@basenode2 ~]# ntpdate 192.168.88.110
    27 Aug 10:05:48 ntpdate[1612]: adjust time server 192.168.88.110 offset -0.000530 sec
    ```

    

## **7.** **用户-组-权限**

### **7.1.** **用户**

- 新增用户
  - useradd luckyboy
  - 会创建同名的组和家目录
- 设置密码
  - passwd luckyboy
- 删除用户
  - userdel -r luckyboy
  - 级联删除家目录和组

- 修改用户信息

  - `usermod -l luckyss luckyls` 修改用户名
    - 家目录和组名称是不会被修改的
  - usermod -L luckyss 锁定用户名
  - usermod -U luckyss 解锁用户名

- 常用文件

  - cat /etc/shadow
    - 用户名和密码
  - cat /etc/passwd
    - 用户名，编号,组编号,家目录，命令，目录
    - 6.5系统0-499 普通 500+
    - 7.6系统0-999 普通 1000+

- 切换账户

  - su hud

    ```sh
    [root@basenode2 ~]# su hud
    [hud@basenode2 ~]$ pwd
    /home/hud
    ```

**添加/删除用户都只能超级管理员用户才有权限**



### **7.2.** **组**

- 创建组

  - ```sh
    groupadd lucky
    ```

- 删除组

  - ```sh
    groupdel lucky
    ```

- 修改组名字

  - ```sh
    groupmod -n school lucky
    ```

- 查看用户对应的组

  - ```sh
    groups
    ```

  - ```sh
    groups schoolboy
    ```

    - 当我们创建用户的时候，会默认创建一个同名的主组

- 修改用户的组

  - ```sh
    - usermod -g lucky schoolboy (主组)
    - usermod -G lucky schoolls (附属组)
    ```

    

### **7.3.** **权限**

![image-20220827110509899](C:\Users\Hud\AppData\Roaming\Typora\typora-user-images\image-20220827110509899.png)

- 查看文件的权限

  - ```sh
    [root@basenode1 ~]# ll
    total 16
    -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
    -rw-r--r--  1 root root 2381 Aug 26 21:36 baidu
    drwxr-xr-x  2 root root   24 Aug 26 19:20 base1
    -rw-r--r--  1 root root  383 Aug 25 21:42 base1.zip
    -rw-r--r--  1 root root   32 Aug 26 00:40 basenode1
    # 三组权限：所属用户权限、所属组的权限、其他人的权限
    ```

  - 三组权限，每组3个字母 

    - r :读取权限
    - w :写入权限
    - x :执行权限
    - -:没有权限

  - root :所属用户(属主)

  - root：所属的组（属组）

  ```sh
  #登录Hud账户
  [Hud@basenode1 ~]$ pwd
  /home/Hud
  [Hud@basenode1 ~]$ ll
  total 0
  #创建一个文件
  [Hud@basenode1 ~]$ touch hudfile
  [Hud@basenode1 ~]$ mkdir games
  [Hud@basenode1 ~]$ ll
  total 0
  drwxrwxr-x 2 Hud Hud 6 Aug 27 14:42 games
  -rw-rw-r-- 1 Hud Hud 0 Aug 27 14:40 hudfile
  
  #如果我想用别的用户访问到
  [Monica@basenode1 ~]$ cd /home/Hud
  -bash: cd: /home/Hud: Permission denied		#被拒绝
  
  #查看权限
  drwx------ 3 Hud    Hud    90 Aug 27 14:42 Hud
  drwx------ 2 Monica Monica 62 Aug 27 14:47 Monica
  ```

- 权限的**UGO**模型（**User、Group、Other**）

  - 三组权限
  - 属主的权限：属组的权限：其他的权限
  - 所有说：将来修改文件的权限 可以从rwx和ugo两个方面进行修改

- **修改文件的权限两种方法**

  - **修改文件所属  `chown`**

    - ```sh
      # 現在文件属于root用户
      [Hud@basenode1 opt]$ ll
      total 4
      -rw-r--r-- 1 root root 26 Aug 27 15:02 aaa
      
      #root用户下进行更改
      [root@basenode1 opt]# chown Hud aaa
      [root@basenode1 opt]# ll
      total 4
      -rw-r--r-- 1 Hud root 26 Aug 27 15:02 aaa
      ```

  - **修改文件的rwx**

    - `chmod o+w aaa`

      ```sh
      [root@basenode1 opt]# ll
      total 4
      -rw-r--rw- 1 Hud root 26 Aug 27 15:02 aaa
      # other多了w权限
      ```

    - `chmod ug+rw aaa`

      ```sh
      [root@basenode1 opt]# chmod ug+rw aaa
      [root@basenode1 opt]# ll
      total 4
      -rw-rw-rw- 1 Hud root 26 Aug 27 15:02 aaa
      ```

    - `chmod ugo-rw aaa`

      ```sh
      # 移除权限
      [root@basenode1 opt]# chmod ugo-rw aaa
      [root@basenode1 opt]# ll
      total 4
      ---------- 1 Hud root 26 Aug 27 15:02 aaa
      ```

    - （权限`RWX`分别对应数字 4 2 1 5= 4+0+1 r-x）

      - `chmod 777 aaa ->(rw- rw-r--)`

        ```sh
        [root@basenode1 opt]# chmod 777 aaa
        [root@basenode1 opt]# ll
        total 4
        -rwxrwxrwx 1 Hud root 26 Aug 27 15:02 aaa
        ```

        

### **7.4.** **权限赋予**

- 我们可以将管理用的权限分配给普通用户
- 文件位置在 vim /etc/sudoers
- 但是修改这个文件需要使用命令
  - visudo
  - 修改 Line 99
    - n1 ALL=(root) /sbin/useradd
    - n1 ALL=(root) /sbin/*
- 如何使用
  - `su n1`
  - `sudo chkconfig iptables off`



## **8.** **管道与重定向**

### **8.1.** **管道**

将前面命令的结果作为参数传递给后面的命令

**`grep`**

- 强大的文本搜索工具

- cat profile | grep if

  ```sh
  [root@basenode1 ~]# cat /etc/profile | grep if
              if [ "$2" = "after" ] ; then
  if [ -x /usr/bin/id ]; then
      if [ -z "$EUID" ]; then
  if [ "$EUID" = "0" ]; then
  if [ "$HISTCONTROL" = "ignorespace" ] ; then
  if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then
      if [ -r "$i" ]; then
          if [ "${-#*i}" != "$-" ]; then 
  ```

- ls / | grep ^t

  ```shell
  [root@basenode1 ~]# ls / | grep ^t
  tmp
  ```

### **8.2.** **重定向**

- 改变数据输出的位置，方向

- 0 in 1 out 2 err

  - ls / 1> lucky 标准输出

  - ls / > lucky 标准输出

  - ls abcd 2>lucky 错误输出

    ```sh
    [root@basenode1 ~]# ll ~ > test
    # 这里也就是将结果输出到了test文件中
    [root@basenode1 ~]# cat test 
    total 12
    -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
    drwxr-xr-x  2 root root   24 Aug 26 19:20 base1
    -rw-r--r--  1 root root  383 Aug 25 21:42 base1.zip
    -rw-r--r--  1 root root   32 Aug 26 00:40 basenode1
    -rw-r--r--  1 root root    0 Aug 27 16:46 test
    
    #2是传递错误信息 报错信息被传进定向文件
    [root@basenode1 ~]# ll base 2> test 
    [root@basenode1 ~]# cat test 
    ls: cannot access base: No such file or directory
    
    # 将另外的内容定向至这个文件 这里发现文件的内容被覆盖了
    [root@basenode1 ~]# ll base1 > test 
    [root@basenode1 ~]# cat test 
    total 4
    -rw-r--r-- 1 root root 64 Aug 25 21:42 readme.txt
    
    ```

- \> 替换 >> 追加

  - **ls / 1>> lucky**

  - **ls / 1> lucky**

- 结合使用（**>> log  2>&1**）

  - ```sh
    [root@basenode1 ~]# ll ~/test1 >> log  2>&1
    [root@basenode1 ~]# cat log 
    ls: cannot access /root/test1: No such file or directory
    [root@basenode1 ~]# ll ~/test >> log  2>&1
    [root@basenode1 ~]# cat log 
    ls: cannot access /root/test1: No such file or directory
    -rw-r--r-- 1 root root 50 Aug 27 16:51 /root/test
    ```

- **信息黑洞**

  - ls /etc /abc >> /dev/null 2>&1（**主要用于清理打印数据，写入/dev/null文件中**）
  - 比如安装一个软件的过程当中，我们不想要安装的信息输出到屏幕上面，也不想动手去清理输出文件。这个时候就可以用到信息黑洞。




## **9. Linux**的系统进程

### **9.1.** **进程信息**

- **`ps -ef`**

  - UID PID PPID C STIME TTY TIME CMD

  - UID 所属用户

  - PID 当前进程编号

  - PPID 当前进程编号的父进程编号

    ```sh
    [root@basenode1 ~]# ps -ef
    UID         PID   PPID  C STIME TTY          TIME CMD
    root          1      0  0 09:19 ?        00:00:01 /usr/lib/systemd/systemd --switched-root --system --deserialize 22
    root          2      0  0 09:19 ?        00:00:00 [kthreadd]
    root          3      2  0 09:19 ?        00:00:00 [kworker/0:0]
    root          4      2  0 09:19 ?        00:00:00 [kworker/0:0H]
    root          6      2  0 09:19 ?        00:00:00 [ksoftirqd/0]
    root          7      2  0 09:19 ?        00:00:00 [migration/0]
    root          8      2  0 09:19 ?        00:00:00 [rcu_bh]
    root          9      2  0 09:19 ?        00:00:00 [rcu_sched]
    root         10      2  0 09:19 ?        00:00:00 [lru-add-drain]
    root         11      2  0 09:19 ?        00:00:00 [watchdog/0]
    root         12      2  0 09:19 ?        00:00:00 [watchdog/1]
    root         13      2  0 09:19 ?        00:00:00 [migration/1]
    root         14      2  0 09:19 ?        00:00:00 [ksoftirqd/1]
    root         16      2  0 09:19 ?        00:00:00 [kworker/1:0H]
    root         17      2  0 09:19 ?        00:00:00 [watchdog/2]
    root         18      2  0 09:19 ?        00:00:00 [migration/2]
    root         19      2  0 09:19 ?        00:00:00 [ksoftirqd/2]
    root         20      2  0 09:19 ?        00:00:00 [kworker/2:0]
    root         21      2  0 09:19 ?        00:00:00 [kworker/2:0H]
    root         22      2  0 09:19 ?        00:00:00 [watchdog/3]
    root         23      2  0 09:19 ?        00:00:00 [migration/3]
    root         24      2  0 09:19 ?        00:00:00 [ksoftirqd/3]
    root         26      2  0 09:19 ?        00:00:00 [kworker/3:0H]
    root         27      2  0 09:19 ?        00:00:00 [watchdog/4]
    root         28      2  0 09:19 ?        00:00:00 [migration/4]
    ```

- **`ps -ef | grep redis`**

  - ```sh
    [root@basenode1 ~]# ps -ef | grep redis
    root       1581   1512  0 09:35 pts/0    00:00:00 grep --color=auto redis
    
    
    ```

- **`ps -aux`**

  - 所有信息

  - ```sh
    [root@basenode1 ~]# ps -aux
    USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root          1  0.1  0.1 191308  4296 ?        Ss   09:19   0:01 /usr/lib/systemd/systemd --switched-root --system --deserialize 22
    root          2  0.0  0.0      0     0 ?        S    09:19   0:00 [kthreadd]
    root          3  0.0  0.0      0     0 ?        S    09:19   0:00 [kworker/0:0]
    root          4  0.0  0.0      0     0 ?        S<   09:19   0:00 [kworker/0:0H]
    root          6  0.0  0.0      0     0 ?        S    09:19   0:00 [ksoftirqd/0]
    root          7  0.0  0.0      0     0 ?        S    09:19   0:00 [migration/0]
    root          8  0.0  0.0      0     0 ?        S    09:19   0:00 [rcu_bh]
    root          9  0.0  0.0      0     0 ?        S    09:19   0:00 [rcu_sched]
    root         10  0.0  0.0      0     0 ?        S<   09:19   0:00 [lru-add-drain]
    root         11  0.0  0.0      0     0 ?        S    09:19   0:00 [watchdog/0]
    root         12  0.0  0.0      0     0 ?        S    09:19   0:00 [watchdog/1]
    root         13  0.0  0.0      0     0 ?        S    09:19   0:00 [migration/1]
    ```

- **`ps -aux --sort -pcpu(CPU使用率排序)`**

  ```sh
  [root@basenode1 ~]# ps -aux --sort -pcpu
  USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root        759  0.2  0.1 272972  4776 ?        Ssl  09:19   0:02 /usr/bin/vmtoolsd
  root          1  0.1  0.1 191308  4296 ?        Ss   09:19   0:01 /usr/lib/systemd/systemd --switched-root --system --deserialize 22
  root        586  0.1  0.1  47920  4368 ?        Ss   09:19   0:01 /usr/lib/systemd/systemd-udevd
  root          2  0.0  0.0      0     0 ?        S    09:19   0:00 [kthreadd]
  root          3  0.0  0.0      0     0 ?        S    09:19   0:00 [kworker/0:0]
  root          4  0.0  0.0      0     0 ?        S<   09:19   0:00 [kworker/0:0H]
  root          6  0.0  0.0      0     0 ?        S    09:19   0:00 [ksoftirqd/0]
  ```

- **`ps  -aux --sort -pmem(内存使用率排序)`**

  ```sh
  [root@basenode1 ~]# ps -aux --sort -pmem
  USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root       1030  0.0  0.4 574276 17440 ?        Ssl  09:19   0:00 /usr/bin/python2 -Es /usr/sbin/tuned -l -P
  polkitd     773  0.0  0.2 612232 11084 ?        Ssl  09:19   0:00 /usr/lib/polkit-1/polkitd --no-debug
  root        769  0.0  0.2 474216 10760 ?        Ssl  09:19   0:00 /usr/sbin/NetworkManager --no-daemon
  root       1032  0.0  0.2 222740  8880 ?        Ssl  09:19   0:00 /usr/sbin/rsyslogd -n
  root       1510  0.0  0.1 161512  6084 ?        Ss   09:20   0:00 sshd: root@pts/0
  root       1590  0.0  0.1 161512  6080 ?        Ss   09:41   0:00 sshd: root@pts/1
  root        758  0.0  0.1 168144  5036 ?        Ss   09:19   0:00 /usr/bin/VGAuthService -s
  root        759  0.2  0.1 272972  4776 ?        Ssl  09:19   0:03 /usr/bin/vmtoolsd
  root        586  0.0  0.1  47920  4368 ?        Ss   09:19   0:01 /usr/lib/systemd/systemd-udevd
  root       1029  0.0  0.1 112900  4316 ?        Ss   09:19   0:00 /usr/sbin/sshd -D
  root          1  0.1  0.1 191308  4296 ?        Ss   09:19   0:01 /usr/lib/systemd/systemd --switched-root --system --deserialize 22
  postfix    1227  0.0  0.1  89880  4084 ?        S    09:19   0:00 qmgr -l -t unix -u
  postfix    1226  0.0  0.1  89812  4060 ?        S    09:19   0:00 pickup -l -t unix -u
  ```

- **`top`**

  - **当前服务器内存使用率**

    ```sh
    [root@basenode1 ~]# top
    top - 09:48:04 up 28 min,  2 users,  load average: 0.06, 0.07, 0.05
    Tasks: 151 total,   1 running, 149 sleeping,   1 stopped,   0 zombie
    %Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 99.5 id,  0.5 wa,  0.0 hi,  0.0 si,  0.0 st
    KiB Mem :  3861288 total,  3474880 free,   259832 used,   126576 buff/cache
    KiB Swap:  8388604 total,  8388604 free,        0 used.  3412108 avail Mem 
    
       PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                                                                                                                                                                    
       759 root      20   0  272972   4776   3652 S   0.3  0.1   0:04.08 vmtoolsd                                                                                                                                                                   
         1 root      20   0  191308   4296   2568 S   0.0  0.1   0:01.93 systemd                                                                                                                                                                    
         2 root      20   0       0      0      0 S   0.0  0.0   0:00.01 kthreadd                                                                                                                                                                   
         3 root      20   0       0      0      0 S   0.0  0.0   0:00.00 kworker/0:0                                                                                                                                                                
         4 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 kworker/0:0H                                                                                                                                                               
         6 root      20   0       0      0      0 S   0.0  0.0   0:00.00 ksoftirqd/0                                                                                                                                                                
         7 root      rt   0       0      0      0 S   0.0  0.0   0:00.05 migration/0                                                                                                                                                                
         8 root      20   0       0      0      0 S   0.0  0.0   0:00.00 rcu_bh                                                                                                                                                                     
         9 root      20   0       0      0      0 S   0.0  0.0   0:00.24 rcu_sched                                                                                                                                                                  
        10 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 lru-add-drain                                                                                                                                                              
        11 root      rt   0       0      0      0 S   0.0  0.0   0:00.01 watchdog/0                                                                                                                                                                 
        12 root      rt   0       0      0      0 S   0.0  0.0   0:00.00 watchdog/1                                                                                                                                                                 
        13 root      rt   0       0      0      0 S   0.0  0.0   0:00.04 migration/1                 
    ```

- **查看进程文件夹**

  ```sh
  [root@basenode1 ~]# cd /proc/
  [root@basenode1 proc]# ll -l
  total 0
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 1
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 10
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 1029
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 1030
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 1032
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 11
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:33 1103
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 1179
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 12
  dr-xr-xr-x  9 postfix postfix               0 Aug 29 09:19 1226
  dr-xr-xr-x  9 postfix postfix               0 Aug 29 09:19 1227
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 13
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 133
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:33 1354
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 137
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 14
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:33 1506
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:20 1510
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:20 1512
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:33 1533
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:34 1549
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:41 1587
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:41 1590
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:41 1592
  dr-xr-xr-x  9 root    root                  0 Aug 29 09:19 16
  ```

  进程开启的时候，进程的文件夹就被创建了。里面存放着进程上下文的数据。

### **9.2.** **后台进程**

**后台运行，至少不会卡在这个界面**

- 只需要在命令的后面添加一个 & 符号

  - `ping www.baidu.com >> baidu &`

    ```sh
    [root@basenode1 ~]# ping baidu.com >>bailog &
    [1] 1644
    [root@basenode1 ~]# ps -ef | grep 1644
    root       1644   1592  0 10:02 pts/1    00:00:00 ping baidu.com
    ```

- jobs -l

  - 可以查看当前的后台进程

  - 但是只有当前用户界面可以获取到

  - ```sh
    [root@basenode1 ~]# jobs -l
    [1]+  1644 Running                 ping baidu.com >> bailog &
    ```

- nohup 可以防止后台进程被挂起

  - `nohup ping www.baidu.com >> baidu 2>&1 &`

#### **9.3.** **杀死进程**

**`kill -9 [进程号]`**

```sh
[root@basenode1 ~]# ps -ef | grep baidu
root       1644   1592  0 10:02 pts/1    00:00:00 ping baidu.com
root       1651   1512  0 10:08 pts/0    00:00:00 grep --color=auto baidu
[root@basenode1 ~]# kill -9 1644
```



## **10. Linux的软件安装**

### **10.1.** **环境变量**

- 当我们执行一个命令的时候，默认从当前路径开始查找
- 如果当前路径找不到对应的命令文件，从环境变量$PATH查找
- $PATH的配置文件在 /etc/profile（系统变量.）
- window 路径与路径之间用;(分号)连接
- Linux路径与路径之间用:（冒号）连接 
- Linux每次修改完成之后，需要重新加载文件 source /etc/profile



### **10.2** **软件的安装方式**

- 解压就可以使用
- 使用安装包安装(window-exe ，Linux-rpm)
  - 自己下载安装包
  - 使用统一的软件帮助我们安装
- 通过源码安装

### **10.3 RPM**安装

- **RedHat Package Manager,它属于红帽的一种包管理方式**

- 通过RPM命令安装软件

  - `rpm -ivh`

  - ```sh
    [root@basenode1 ~]# rpm -ivh jdk-8u231-linux-x64.rpm 
    warning: jdk-8u231-linux-x64.rpm: Header V3 RSA/SHA256 Signature, key ID ec551f03: NOKEY
    Preparing...                          ################################# [100%]
    Updating / installing...
       1:jdk1.8-2000:1.8.0_231-fcs        ################################# [100%]
    Unpacking JAR files...
    	tools.jar...
    	plugin.jar...
    	javaws.jar...
    	deploy.jar...
    	rt.jar...
    	jsse.jar...
    	charsets.jar...
    	localedata.jar...
    ```

- 可以查询软件

  - rpm -qa | grep jdk

    ```sh
    [root@basenode1 ~]# rpm -qa | grep jdk
    jdk1.8-1.8.0_231-fcs.x86_64
    ```

  - rpm -q jdk

- 卸载

  - `rpm -e jdk-1.7.0_67-fcs.x86_64`

- 需要手动配置Java的环境变量

  - `vim /etc/profile`

  - ```sh
    export JAVA_HOME=/usr/java/jdk1.7.0_67
    export PATH=$JAVA_HOME/bin:$PATH
    ```

- 重新加载配置文件

  - `source /etc/profile`



### **10.4.** **压缩包解压安装**

- 解压文件

  - `tar -zxf apache-tomcat-7.0.61.tar.gz`

- 拷贝到/opt/school目录下

  - mkdir -p /opt/lucky
  - cp -r apache-tomcat-7.0.61 /opt/school

- 启动**tomcat**

  - cd /opt/school/apache-tomcat-7.0.61/bin/

  - ./startup.sh

  - ```sh
    [root@basenode1 bin]# ./startup.sh
    Using CATALINA_BASE:   /opt/apache-tomcat-8.5.47
    Using CATALINA_HOME:   /opt/apache-tomcat-8.5.47
    Using CATALINA_TMPDIR: /opt/apache-tomcat-8.5.47/temp
    Using JRE_HOME:        /usr/java/jdk1.8.0_231-amd64
    Using CLASSPATH:       /opt/apache-tomcat-8.5.47/bin/bootstrap.jar:/opt/apache-tomcat-8.5.47/bin/tomcat-juli.jar
    Tomcat started.
    ```

    **查看一下进程信息**：

    ```sh
    [root@basenode1 bin]# ps -ef | grep tomcat
    root       8016      1 12 13:51 pts/2    00:00:04 /usr/java/jdk1.8.0_231-amd64/bin/java -Djava.util.logging.config.file=/opt/apache-tomcat-8.5.47/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Djdk.tls.ephemeralDHKeySize=2048 -Djava.protocol.handler.pkgs=org.apache.catalina.webresources -Dorg.apache.catalina.security.SecurityListener.UMASK=0027 -Dignore.endorsed.dirs= -classpath /opt/apache-tomcat-8.5.47/bin/bootstrap.jar:/opt/apachetomcat-8.5.47/bin/tomcat-juli.jar -Dcatalina.base=/opt/apache-tomcat-8.5.47 -Dcatalina.home=/opt/apache-tomcat-8.5.47 -Djava.io.tmpdir=/opt/apache-tomcat-8.5.47/temp org.apache.catalina.startup.Bootstrap start
    root       8101   4095  0 13:52 pts/2    00:00:00 grep --color=auto tomcat
    ```

    进入主机的来看浏览器，访问http://192.168.88.110:8080

    ![image-20220829135854098](C:\Users\Hud\AppData\Roaming\Typora\typora-user-images\image-20220829135854098.png)

​					这里的Hud是修改了`[root@basenode1 bin]# vi ../webapps/ROOT/index.jsp`下的文件



### **10.5 YUM**安装

#### **10.5.1 yum**的作用

- 可以帮我们管理RPM包
- 可以帮我们安装软件，
- 如果软件有其他依赖，会帮我们安装依赖后在安装软件
- 类似于Maven



#### 10.5.2  yum命令

- search 查询命令或者软件
- info
  - 查看包的信息
- list / list jdk
  - 查询安装的rpm包，或者只查询某一周



#### 10.5.3 更换yum源

- **首先安装wget**

  - ```sh
    yum install wget -y
    ```

- **将系统原始配置文件失效**

  - `mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup`

  ```sh
  [root@basenode1 yum.repos.d]# mv /etc/yum.repos.d/CentOS-Base.repo  /etc/yum.repos.d/CentOS-Base.repo.backup
  [root@basenode1 yum.repos.d]# ll
  total 40
  -rw-r--r--. 1 root root 1664 Oct 23  2020 CentOS-Base.repo.backup
  -rw-r--r--. 1 root root 1309 Oct 23  2020 CentOS-CR.repo
  -rw-r--r--. 1 root root  649 Oct 23  2020 CentOS-Debuginfo.repo
  -rw-r--r--. 1 root root  314 Oct 23  2020 CentOS-fasttrack.repo
  -rw-r--r--. 1 root root  630 Oct 23  2020 CentOS-Media.repo
  -rw-r--r--. 1 root root 1331 Oct 23  2020 CentOS-Sources.repo
  -rw-r--r--. 1 root root 8515 Oct 23  2020 CentOS-Vault.repo
  -rw-r--r--. 1 root root  616 Oct 23  2020 CentOS-x86_64-kernel.repo
  ```

- 使用Wget获取阿里yum源配置文件

  - ```sh
    wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
    ```

- 清空以前yum源的缓存

  - yum clean all

- 获取阿里云的缓存

  - ```sh
    [root@basenode1 ~]# yum makecache
    Loaded plugins: fastestmirror
    Determining fastest mirrors
     * base: mirrors.aliyuncs.com
     * extras: mirrors.aliyuncs.com
     * updates: mirrors.aliyuncs.com
    base                                                                                                                                                                                                                      | 1.6 kB  00:00:00     
    http://mirrors.aliyuncs.com/centos/7/os/x86_64/repodata/repomd.xml: [Errno -1] Error importing repomd.xml for base: Damaged repomd.xml file
    Trying other mirror.
    base                                                                                                                                                                                                                      | 3.6 kB  00:00:00     
    extras                                                                                                                                                                                                                    | 2.9 kB  00:00:00     
    updates                                                                                                                                                                                                                   | 2.9 kB  00:00:00     
    base/7/x86_64/filelists_db     FAILED                                          
    http://mirrors.cloud.aliyuncs.com/centos/7/os/x86_64/repodata/d6d94c7d406fe7ad4902a97104b39a0d8299451832a97f31d71653ba982c955b-filelists.sqlite.bz2: [Errno 14] curl#6 - "Could not resolve host: mirrors.cloud.aliyuncs.com; Unknown error" ETA 
    Trying other mirror.
    base/7/x86_64/other_db         FAILED                                          
    http://mirrors.cloud.aliyuncs.com/centos/7/os/x86_64/repodata/ecaab5cc3b9c10fefe6be2ecbf6f9fcb437231dac3e82cab8d9d2cf70e99644d-other.sqlite.bz2: [Errno 14] curl#6 - "Could not resolve host: mirrors.cloud.aliyuncs.com; Unknown error"-:-- ETA 
    Trying other mirror.
    (1/10): base/7/x86_64/group_gz                                                                                                                                                                                            | 153 kB  00:00:00     
    (2/10): extras/7/x86_64/primary_db                                                                                                                                                                                        | 247 kB  00:00:00     
    (3/10): extras/7/x86_64/filelists_db                                                                                                                                                                                      | 277 kB  00:00:00     
    (4/10): extras/7/x86_64/other_db                                                                                                                                                                                          | 148 kB  00:00:00     
    (5/10): base/7/x86_64/primary_db                                                                                                                                                                                          | 6.1 MB  00:00:12     
    (6/10): updates/7/x86_64/filelists_db                                                                                                                                                                                     | 9.4 MB  00:00:19     
    (7/10): updates/7/x86_64/other_db                                                                                                                                                                                         | 1.1 MB  00:00:02     
    (8/10): base/7/x86_64/other_db                                                                                                                                                                                            | 2.6 MB  00:00:06     
    (9/10): updates/7/x86_64/primary_db                                                                                                                                                                                       |  17 MB  00:00:37     
    (10/10): base/7/x86_64/filelists_db                                                                                                                                                                                       | 7.2 MB  00:00:17     
    Metadata Cache Created
    
    ```

### 10.6 Linux yum 命令

yum是一个在 Fedora 和 RedHat 以及 SUSE 中的 Shell 前端软件包管理器。

基于 RPM 包管理，能够从指定的服务器自动下载 RPM 包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。

yum 提供了查找、安装、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

- #### yum 语法

```
yum [options] [command] [package ...]
```

- **options：**可选，选项包括-h（帮助），-y（当安装过程提示选择全部为 "yes"），-q（不显示安装的过程）等等。
- **command：**要进行的操作。
- **package：**安装的包名。

------

- ## yum常用命令

  - 列出所有可更新的软件清单命令：**yum check-update**

  - 更新所有软件命令：**yum update**

  - 仅安装指定的软件命令：**yum install <package_name>**

  - 仅更新指定的软件命令：**yum update <package_name>**

  - 列出所有可安裝的软件清单命令：**yum list**

  - 删除软件包命令：**yum remove <package_name>**

  - 查找软件包命令：**yum search <keyword>**

  - 清除缓存命令:
    - **yum clean packages**: 清除缓存目录下的软件包
    - **yum clean headers**: 清除缓存目录下的 headers
    - **yum clean oldheaders**: 清除缓存目录下旧的 headers
    - **yum clean, yum clean all (= yum clean packages; yum clean oldheaders)** :清除缓存目录下的软件包及旧的 headers


## **11. Linux的三剑客**

### **11.1  **普通剑客**

- - **cut**

    - 用指定的规则来切分文本

    - 下面实例 `cut -d ':'` 意思就是用：进行切分，`-f1,2,3,4,5`意思是获取切分的第1,2,3,4,5列

      ```sh
      [root@basenode1 ~]# cut -d ':' -f1,2,3,4,5  passwd |grep root 
      root:x:0:0:root
      [root@basenode1 ~]# cut -d ':' -f1,2,3,4,5  passwd 
      root:x:0:0:root
      bin:x:1:1:bin
      daemon:x:2:2:daemon
      adm:x:3:4:adm
      lp:x:4:7:lp
      sync:x:5:0:sync
      shutdown:x:6:0:shutdown
      halt:x:7:0:halt
      mail:x:8:12:mail
      operator:x:11:0:operator
      games:x:12:100:games
      ftp:x:14:50:FTP User
      nobody:x:99:99:Nobody
      systemd-network:x:192:192:systemd Network Management
      dbus:x:81:81:System message bus
      polkitd:x:999:998:User for polkitd
      sshd:x:74:74:Privilege-separated SSH
      postfix:x:89:89:
      ntp:x:38:38:
      Hud:x:1000:1000:
      Monica:x:1001:1001:
      ```

  - **sort**

    - `sort [filename]`

      - 对文本中的行进行排序

      ```sh
      [root@basenode1 ~]# sort passwd 
      adm:x:3:4:adm:/var/adm:/sbin/nologin
      bin:x:1:1:bin:/bin:/sbin/nologin
      daemon:x:2:2:daemon:/sbin:/sbin/nologin
      dbus:x:81:81:System message bus:/:/sbin/nologin
      ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
      games:x:12:100:games:/usr/games:/sbin/nologin
      halt:x:7:0:halt:/sbin:/sbin/halt
      Hud:x:1000:1000::/home/Hud:/bin/bash
      lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
      mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
      Monica:x:1001:1001::/home/Monica:/bin/bash
      nobody:x:99:99:Nobody:/:/sbin/nologin
      ntp:x:38:38::/etc/ntp:/sbin/nologin
      operator:x:11:0:operator:/root:/sbin/nologin
      polkitd:x:999:998:User for polkitd:/:/sbin/nologin
      postfix:x:89:89::/var/spool/postfix:/sbin/nologin
      root:x:0:0:root:/root:/bin/bash
      shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
      sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
      sync:x:5:0:sync:/sbin:/bin/sync
      systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
      ```

    - `sort -t':' -k[n] [filename]`

      - **对每一行的数据进行切分，按照第3列进行排序**

      ```sh
      [root@basenode1 ~]# sort -t':' -k3 passwd 
      root:x:0:0:root:/root:/bin/bash
      Hud:x:1000:1000::/home/Hud:/bin/bash
      Monica:x:1001:1001::/home/Monica:/bin/bash
      operator:x:11:0:operator:/root:/sbin/nologin
      bin:x:1:1:bin:/bin:/sbin/nologin
      games:x:12:100:games:/usr/games:/sbin/nologin
      ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
      systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
      daemon:x:2:2:daemon:/sbin:/sbin/nologin
      adm:x:3:4:adm:/var/adm:/sbin/nologin
      ntp:x:38:38::/etc/ntp:/sbin/nologin
      lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
      sync:x:5:0:sync:/sbin:/bin/sync
      shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
      halt:x:7:0:halt:/sbin:/sbin/halt
      sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
      mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
      dbus:x:81:81:System message bus:/:/sbin/nologin
      postfix:x:89:89::/var/spool/postfix:/sbin/nologin
      polkitd:x:999:998:User for polkitd:/:/sbin/nologin
      nobody:x:99:99:Nobody:/:/sbin/nologin
      ```

    - `sort -t':' -k3 -r [filename]`

      - 逆序(这里和上面都是按字符串排序的)

      - ```sh
        [root@basenode1 ~]# sort -t':' -k3 -r passwd 
        nobody:x:99:99:Nobody:/:/sbin/nologin
        polkitd:x:999:998:User for polkitd:/:/sbin/nologin
        postfix:x:89:89::/var/spool/postfix:/sbin/nologin
        dbus:x:81:81:System message bus:/:/sbin/nologin
        mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
        sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
        halt:x:7:0:halt:/sbin:/sbin/halt
        shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
        sync:x:5:0:sync:/sbin:/bin/sync
        lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
        ntp:x:38:38::/etc/ntp:/sbin/nologin
        adm:x:3:4:adm:/var/adm:/sbin/nologin
        daemon:x:2:2:daemon:/sbin:/sbin/nologin
        systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
        ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
        games:x:12:100:games:/usr/games:/sbin/nologin
        bin:x:1:1:bin:/bin:/sbin/nologin
        operator:x:11:0:operator:/root:/sbin/nologin
        Monica:x:1001:1001::/home/Monica:/bin/bash
        Hud:x:1000:1000::/home/Hud:/bin/bash
        root:x:0:0:root:/root:/bin/bash
        ```

    - `sort -t' ' -k2 -n lucky`

      - **按照数值大小进行排序,如果有字母，字母在前(按数值排序了)**

      ```sh
      [root@basenode1 ~]# sort -t':' -k3 -n passwd 
      root:x:0:0:root:/root:/bin/bash
      bin:x:1:1:bin:/bin:/sbin/nologin
      daemon:x:2:2:daemon:/sbin:/sbin/nologin
      adm:x:3:4:adm:/var/adm:/sbin/nologin
      lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
      sync:x:5:0:sync:/sbin:/bin/sync
      shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
      halt:x:7:0:halt:/sbin:/sbin/halt
      mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
      operator:x:11:0:operator:/root:/sbin/nologin
      games:x:12:100:games:/usr/games:/sbin/nologin
      ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
      ntp:x:38:38::/etc/ntp:/sbin/nologin
      sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
      dbus:x:81:81:System message bus:/:/sbin/nologin
      postfix:x:89:89::/var/spool/postfix:/sbin/nologin
      nobody:x:99:99:Nobody:/:/sbin/nologin
      systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
      polkitd:x:999:998:User for polkitd:/:/sbin/nologin
      Hud:x:1000:1000::/home/Hud:/bin/bash
      Monica:x:1001:1001::/home/Monica:/bin/bash
      ```

- **wc**

  - 统计单词的数量

  - **wc passwd**

    ```sh
    [root@basenode1 ~]# wc passwd 
     21  29 914 passwd			#分別代表  行 单词数 字符数
    ```

- **-l line**

- **-w word 以空格来分割单词**

- **-c char**



### 11.2 剑客1号：grep

- 可以对文本进行搜索

- 同时搜索多个文件

  - **从文档中查询指定的数据**

    ```sh
    [root@basenode1 ~]# grep Hud passwd 
    Hud:x:1000:1000::/home/Hud:/bin/bash
    ```

  - **从多个文件中查询（`grep xxx [filename1] [filename2]` ）**

    ```sh
    [root@basenode1 ~]# grep Hud passwd test 
    passwd:Hud:x:1000:1000::/home/Hud:/bin/bash
    test:this is Hud typing
    ```

- **显示匹配的行号(-n)**

  - `grep -n Hud passwd`

    ```sh
    [root@basenode1 ~]# grep -n Hud passwd
    20:Hud:x:1000:1000::/home/Hud:/bin/bas
    ```

- 显示不匹配的忽略大小写

  - `grep -i Hud passwd `

    ```sh
    [root@basenode1 ~]# grep -i Hud test 
    this is Hud typing
    hud is talking 
    ```

- 使用正则表达式匹配

  - ```sh
    [root@basenode1 ~]# grep -E "[1-2]" passwd
    bin:x:1:1:bin:/bin:/sbin/nologin
    daemon:x:2:2:daemon:/sbin:/sbin/nologin
    mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
    operator:x:11:0:operator:/root:/sbin/nologin
    games:x:12:100:games:/usr/games:/sbin/nologin
    ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
    systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
    dbus:x:81:81:System message bus:/:/sbin/nologin
    Hud:x:1000:1000::/home/Hud:/bin/bash
    Monica:x:1001:1001::/home/Monica:/bin/bash
    ```



### **11.3 剑客2号：sed**

- sed 是Stream Editor（字符流编辑器）的缩写，简称流编辑器
- Sed软件从文件或管道中读取一行，处理一行，输出一行；再读取一行，再处理一行，再输出一行...
- 一次一行的设计使得sed软件性能很高
- vi命令打开文件是一次性将文件加载到内存
- 了解即可
  - https://www.cnblogs.com/chensiqiqi/p/6382080.html

- **行的选择模式**
  - 10 第十行
  - m,n --> 第m行到第n行 [m,n]
  - m,+n-->第一行到第四行 [m,m+n]
  - m~n-->从m行开始，依次累加n
  - m,$ -->从m开始到最后一行
  - /school/ -->匹配到school的行
  - /u1/,/u4/-->从匹配u1到匹配u4

- 增

  - ```sh
    [root@basenode1 ~]# sed 'a Lebron James is King~' test 
    this is Hud typing
    Lebron James is King~
    hud is talking 
    Lebron James is King~
    [root@basenode1 ~]# sed '1a Lebron James is King~' test 
    this is Hud typing
    Lebron James is King~
    hud is talking 
    
    [root@basenode1 ~]# cat test 
    this is Hud typing
    hud is talking 
    ```

    **‘a’ 表示append追加 打印到控制台  但不修改文件** 

  - **`sed -i`**  **直接修改到文件**

    ```sh
    [root@basenode1 ~]# sed -i '1a Lebron James is King~' test 
    [root@basenode1 ~]# cat test 
    this is Hud typing
    Lebron James is King~
    hud is talking 
    ```

- 删

  - **sed '2d' [filename]** 

    ```sh
    # 假删一下
    [root@basenode1 ~]# sed '2d' test 
    this is Hud typing
    hud is talking 
    [root@basenode1 ~]# cat test 
    this is Hud typing
    Lebron James is King~
    hud is talking
    
    # 这里真删
    [root@basenode1 ~]# sed -i '2d' test 
    [root@basenode1 ~]# cat test 
    this is Hud typing
    hud is talking 
    ```

- 改

  - 整行替换

    - ```sh
      [root@basenode1 ~]# cat test 
      this is Hud typing
      hud is talking
      hello
      hi
      how are you 
      [root@basenode1 ~]# sed '3c Hud' test 
      this is Hud typing
      hud is talking
      Hud
      hi
      how are you 
      ```

    - ```sh
      [root@basenode1 ~]# cat test 
      this is Hud typing
      hud is talking
      hello
      hi
      how are you 
      [root@basenode1 ~]# sed '1~1c Hud' test 
      Hud
      Hud
      Hud
      Hud
      Hud
      [root@basenode1 ~]# sed '1~2c Hud' test 
      Hud
      hud is talking
      Hud
      hi
      Hud
      ```

  - **字符替换 sed -i 's/目标内容/替换内容/g' [filename]**

    ```sh
    [root@basenode1 ~]# cat test 
    this is Hud typing
    hud is talking
    hello
    hi
    how are you 
    [root@basenode1 ~]# sed '1,5s/Hud/Monica/g' test 
    this is Monica typing
    hud is talking
    hello
    hi
    how are you 
    ```



### **11.4 剑客3号：awk**

- 它不是一个剑客，它是一门语言

- 了解即可

  - https://www.cnblogs.com/chensiqiqi/p/6481647.html

- 模式与动作

  - ```sh
    - awk -F ":" 'NR>=2&&NR<=6' /etc/passwd
    - awk -F ":" '{print NR,$1}' /etc/passwd
    - awk -F ":" 'NR>=2&&NR<=6 {print NR,$1}' /etc/passwd
    - awk -F ":" 'NR==1{print NR,$1}NR==2{print NR,$NF}' /etc/passwd
    ```





# shell编程

## 1. shell编程概述

### 1.1 shell名词解释

- **Kernel**

  - Linux内核主要是为了和硬件打交道

- **Shell**

  - 命令解释器（command interpreter）
  - Shell是一个用C语言编写的程序，他是用户使用Linux的桥梁。Shell既是一种命令语言，又是一种程序设计语言
  - Shell是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务

- **Shell的两大主流**

  - sh：
    - Bourne shell (sh) ,Solaris,hpux默认shell
    - Bourne again shell (bash),Linux 系统默认shell
  - csh：
    - C shell(csh)
    - tc shell (tcsh)

- **#! 声明**

  - ```sh
    #! /bin/bash
    ```

  ```sh
  [root@basenode1 ~]# vi hello.sh
  [root@basenode1 ~]# ll
  total 8
  -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
  -rw-r--r--  1 root root   34 Aug 30 16:32 hello.sh
  ```



### 1.2 shell脚本的执行

- 输入脚本文件的绝对路径或相对路径

  - **执行的必须是一个可执行文件**

    ```sh
    [root@basenode1 ~]# ./hello.sh
    -bash: ./hello.sh: Permission denied
    # 现在无法执行 因为还不是脚本 没有执行权限
    [root@basenode1 ~]# chmod 777 hello.sh 
    [root@basenode1 ~]# ll
    total 8
    -rw-------. 1 root root 1537 Aug 23 00:41 anaconda-ks.cfg
    -rwxrwxrwx  1 root root   34 Aug 30 16:32 hello.sh
    #添加完权限后，再看看执行
    [root@basenode1 ~]# ./hello.sh
    hello from Hud!
    ```

- **bash或者sh +脚本**

  ```sh
  [root@basenode1 ~]# sh /root/hello.sh
  hello from Hud!
  ```

- **在脚本的路径前面再加.或者source**

  ```sh
  [root@basenode1 ~]# source hello.sh 
  hello from Hud!
  ```

- **区别**

  - 第一种和第二种会新开一个bash，不同bash中的变量无法共享

  - 第三种是在同一个shell里面执行的

    - #### 很明显看出来 使用sh方式会多增加一个进程

  ```
  [root@basenode1 ~]# sh hello.sh
  root      20882   6648  0 18:07 pts/1    00:00:00 sh hello.sh
  root      20883  20882  0 18:07 pts/1    00:00:00 ping www.baidu.com
  root      20886  20208  0 18:07 pts/0    00:00:00 ps -ef
  
  [root@basenode1 ~]# source hello.sh
  root      20692   6648  0 18:03 pts/1    00:00:00 ping www.baidu.com
  root      20702  20208  0 18:04 pts/0    00:00:00 ps -ef
  ```

  **看个例子：**

  ```sh
  # 关于bash中的变量共享
  [root@basenode1 ~]# name=Hud
  [root@basenode1 ~]# echo $name
  Hud 
  [root@basenode1 ~]# vi hello.sh 
  #! /bin/bash
  echo hello from Hud!
  echo $name
  [root@basenode1 ~]# sh hello.sh 
  hello from Hud!
  
  [root@basenode1 ~]# source hello.sh 
  hello from Hud!
  Hud
  ```

  

- **export：**可以将当前进程的变量传递给子进程去使用，**看看例子**

  - 上面不使用source，子进程中无法获取name变量的值

    这里使用**export**

    ```sh
    [root@basenode1 ~]# export name=Hud
    [root@basenode1 ~]# echo $name
    Hud
    [root@basenode1 ~]# source hello.sh
    hello from Hud!
    Hud
    [root@basenode1 ~]# sh hello.sh
    hello from Hud!
    Hud
    ```

    这里sh时候也可以看到name变量的值了。



## 2. Shell基础入门

### 2.1 shell变量

- **定义变量时，变量名不加$符号**

  - 命名只能使用英文字母、数字和下划线，首个字符不能以数字开头
  - 中间不能有空格，可以使用下划线
  - 不能使用标点符号
  - 不能使用bash里的关键字

- **变量的类型**

  - 局部变量

    - 局部变量在脚本或者命令中定义，仅仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量

  - 环境变量

    - 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行

  - shell变量

    - shell变量是由shell程序设置的特殊变量，shell变量有一部分是环境变量，有一部分是局部变量

    

```shell
# var.sh

#! /bin/bash
# 变量的声明
name=qitianyu
# 变量的调用
echo $name
echo ${name}

#只读变量   /bin/sh: NAME: This variable is read only.
url="www.pronhub.com"
readonly url
url="www.xvideos.com"
-bash: url: readonly variable

# 删除变量 unset
unset url
```



### 2.2 shell字符串

- 字符串是shell编程中最常用最有用的数据类型，字符串可以用单引号，也可以用双引号，也可以不用引号

- 单引号

  - 单引号里面的任何字符都会原样输出，单引号字符串中的变量是无效的
  - 单引号字符串中不能出现单独一个的单引号，但可成对出现，作为字符串拼接使用

- 双引号

  - 双引号里可以有变量
  - 双引号里可以出现转义字符

  ```shell
  # 声明字符串
  str1="hello world 1"
  str2='hello world 2'
  
  # 字符串拼接--双引号
  name='Hud'
  s1="hello,"$name"!"
  s2="hello,${name}!"
  
  # 字符串拼接--单引号
  passwd='199866'
  p1='PW is '$passwd'!'
  p2='PW is ${passwd}!'
  
  # 查看输出
  [root@basenode1 ~]# echo $p1
  PW is 199866!
  [root@basenode1 ~]# echo $p2
  PW is ${passwd}!
  
  # 字符串的长度
  email=qitianyu2007@126.com
  echo ${#email}
  >20
  echo ${email:1:4}
  >itia
  ```



### 2.3 shell数组

- shell支持一维数组（不支持多维数组），并且没有限定数组的大小

- 数组元素的下标由0开始编号。获取组中的元素需要利用下标，下标可以是整数或者算数表达式，值应该大于等于0

- ```sh
  # 定义数组 括号来表示数组，数组元素用空格符号分隔开
  #数组名=(值1 值2 ... 值n)
  Players=("Derrick Rose" "Lebron James" "Kevin Durant")
  
  # 读取数组 ${数组名[下标]}
  favourite=${Players[0]}
  echo favourite     #Derrick Rose
  
  # 使用@符号可以获取数组中的所有元素
  [root@basenode1 ~]# all=${Players[@]}
  [root@basenode1 ~]# echo $all
  Derrick Rose Lebron James Kevin Durant
  
  #获取数组长度
  [root@basenode1 ~]# echo ${#Players[@]}
  3
  [root@basenode1 ~]# echo ${#Players[*]}
  3
  ```

  

### 2.4 shell注释

一般使用#

```sh
# 特殊的多行注释

:<<EOF(!)
注释内容。。。
注释内容。。。
注释内容。。。
注释内容。。。
EOF(!)
```



### 2.5 shell参数传递

- 执行shell脚本时，向脚本传递参数，脚本内获取参数的格式为：**$n，n**代表一个数字

| 参数处理 | 参数说明                                                    |
| -------- | ----------------------------------------------------------- |
| $#       | 传递到脚本的参数个数                                        |
| $*       | 以一个单字符串显示所有向脚本传递的参数                      |
| $$       | 脚本运行的当前进程ID号                                      |
| #!       | 后台运行的最后一个进程的ID号                                |
| #?       | 显示最后命令的退出状态，0表示没有错误，其他任何值表示有错误 |
| #0       | 执行的文件名                                                |

```sh
# hello.sh
#--------------------
#! /bin/bash

echo "hello,$1!"
echo "hello,$2!"
echo "hello,$3!"

echo "参数个数：$#"
echo "脚本当前进程ID：$$"
echo "后台最后一个进程ID：$$"
echo "执行的文件名$0"
```

```sh
[root@basenode1 ~]# sh hello.sh Hud Monica QB
hello,Hud!
hello,Monica!
hello,QB!
参数个数：3
脚本当前进程ID：10839
后台最后一个进程ID：10839
执行的文件名hello.sh
```





## 3. Shell高级进阶

### 3.1 shell运算符

- **shell运算符的分类**

  - **算数运算符**

    | 运算符 | 说明       | 举例           |
    | ------ | ---------- | -------------- |
    | +      | 加法       | `'expr $a+$b'` |
    | -      | 减法       | `'expr $a-$b'` |
    | *      | 乘法       | `'expr $a*$b'` |
    | /      | 除法       | `'expr $a/$b'` |
    | %      | 取余       | `'expr $a/$b'` |
    | =      | 赋值       | '`expr $a%$b'` |
    | ==     | 比较相等？ | `$a ==$b`      |
    | !=     | 比较不等？ | `$a != $b`     |

  - **关系运算符**

    - 关系运算符只支持数字，不支持字符串，除非字符串的值是数字
    - eq(等于)、ne(不等于)、gt(大于)、lt(小于)、ge(大于等于)、le(小于等于)

  - **字符串运算符**

    ```sh
    s1='abc'
    s2='def'
    [$s1 = $s2]    #是否相等
    [$s1 = $s2]	   #是否不等
    if [-z $a]     #字符串长度是否为0 true：为0
    if [-n $a]     #字符串长度是否不为0 true：不为0
    if [$a]		   #字符串是否为空 true：不为空
    ```

  - **文件测试运算符**

    ```sh
    file="~/hello.sh"
    
    if[-r file]   #文件可读？
    if[-w file]	  #文件可写？
    if[-x file]	  #文件可执行？
    if[-f file]	  #文件为普通文件？
    if[-d file]	  #文件为一个目录？
    if[-s file]	  #文件为空？
    if[-e file]	  #文件存在？
    ```



### 3.2 echo打印数据

- 用于字符串的输出

  ```sh
  # 显示普通字符串
  echo "Hud"
  
  # 显示转义字符
  echo "\"Hud\""
  >"Hud"
  
  # 显示变量
  name=Hud
  echo "my name is $name"
  >my name is Hud
  
  # 显示换行
  echo -e "Hello! \n"
  echo "Monica"
  >
  Hello! 
  
  Monica
  
  # 显示不换行
  echo -e "Hello! \c"
  echo "Monica"
  >Hello! Monica
  
  # 显示结果定向至文件
  echo 'hello world' >file
  
  #原样输出字符串
  echo '  *
   * *
  * * *  '
  >
    *
   * *
  * * *
  
  # 显示命令执行结果
  [root@basenode1 network-scripts]# echo `pwd`
  /etc/sysconfig/network-scripts
  ```



### 3.3 文件测试

- 用于检查某个条件是否成立。可以对数值、文件、字符三个方面进行测试。

- ```shell
  if test 判断条件
  ```

​	

### 3.4 流程控制

#### 3.4.1 if

- ```sh
  if condition1 
  then 
  	command1
  elif condition2
  then 
  	command2
  else
  	command3
  fi
  ```



#### 3.4.2 case

- ```sh
  case 值 in
  模式1)
  	command1
  	command2
  	...
  	commandN
  	;;
  模式2)
  	command1
  	command2
  	...
  	commandN
  	;;
  esac
  
  #实例
  echo "请输入1-4之间的一个数字"
  echo "你输入的数字为："
  read num
  case $num in
  	1)ehco "你选择了1"
  	;;
  	2)ehco "你选择了2"
  	;;
  	3)ehco "你选择了3"
  	;;
  	4)ehco "你选择了4"
  	;;
  	*)echo "输入有误"
  	;;
  esac
  
  [root@basenode1 ~]# sh test.sh 
  请输入1-4之间的一个数字
  你输入的数字为：
  2
  你选择了2
  ```

  

#### 3.4.3 for

- 当变量值在列表里，for循环执行一次所有命令，使用变量名获取列表中的当前取值

- 命令可以为任何有效的shell命令和语句，in列表可以包含替换、字符串和文件名

- in列表是可选的，如果不用他，for循环使用命令行的位置参数

  ```sh
  for var in item1,item2,item3...
  do
  	command1
  	command2
  	...
  	commandN
  done
  ```

  ```sh
  for loop in 1 2 3 4 5
  do
  	echo "the value is $loop"
  done
  
  for str in "Hud is typing a string"
  do 
  	echo $str
  done
  
  [root@basenode1 ~]# ./test1.sh 
  the value is 1
  the value is 2
  the value is 3
  the value is 4
  the value is 5
  Hud is typing a string
  ```



#### 3.4.4 while

- while循环不断执行一系列命令，也用于从输入文件中读取数据；命令通常为测试条件。

  ```sh
  while condation
  do 
  	command
  done
  ```

  ```sh
  # Bash let 命令，它用于执行一个或多个表达式，变量计算中不需要加上$来表示变量
  #! /bin/bash
  int=1
  while(($int<5))
  do
  	echo $int
  	let "int++"
  done
  [root@basenode1 ~]# sh test.sh 
  1
  2
  3
  4
  ```

  ```sh
  # 无限循环
  while true
  do
  	command
  done
  ```



#### 3.4.5 break

- break命令运行跳出所有循环（终止执行后面的所有循环）。

  ```sh
  #! /bin/bash
  while :
  do
          echo "输入一个1-5之前的数字"
          read aNum
          case $aNum in
          1|2|3|4|5)
             echo "你输入的数字为$aNum"
          ;;
          *) echo "兄弟你输入有误 over"
          break
          ;;
          esac
  done
  
  [root@basenode1 ~]# sh test.sh 
  输入一个1-5之前的数字
  3
  你输入的数字为3
  输入一个1-5之前的数字
  9
  兄弟你输入有误 over
  ```



#### 3.4.6 continue

- continue命令不会跳出所有循环，仅仅跳出当前循环

  ```sh
  #! /bin/bash
  while :
  do
          echo "输入一个1-5之前的数字"
          read aNum
          case $aNum in
          1|2|3|4|5)
             echo "你输入的数字为$aNum"
          ;;
          *) echo "兄弟你输入有误"
          continue
          echo "游戏结束"
          ;;
          esac
  done
  
  [root@basenode1 ~]# sh test.sh 
  输入一个1-5之前的数字
  3
  你输入的数字为3
  输入一个1-5之前的数字
  7
  兄弟你输入有误
  输入一个1-5之前的数字
  ^C
  ```

  

### 3.5 Shell函数

- linux shell可以用户自定义函数，然后在shell脚本中可以随意调用

- 可以带function func()定义，也可以直接func()定义，不带任何参数

- 参数返回，可以显示加：return返回，如果不加，将以最后一条命令运行结果作为返回值，return后跟数值0~255

  ```sh
  #! /bin/bash
  
  ## 第一个函数-----------
  demoFun(){
  	echo "这是Hud写的第一个"
  }
  echo "函数开始执行"
  demoFun
  echo "函数执行结束"
  
  ## 函数返回值
  funcWithReturn(){
  	echo "这个函数做加法"
  	echo "输入第一个数"
  	read aNum
  	echo "输入第二个数"
  	read bNum
  	return $(($aNum+$bNum))	
  }
  funcWithReturn
  
  ## 函数返回值在调用该函数后通过$?来获得
  echo "两数之和为$?"
  
  [root@basenode1 ~]# sh test.sh 
  函数开始执行---------
  这是Hud写的第一个
  函数执行结束---------
  这个函数做加法
  输入第一个数
  2
  输入第二个数
  3
  两数之和为5
  ```

  **函数参数**

  ```sh
  #! /bin/bash
  funcWithParam(){
  	echo "第一个参数为 $1"
  	echo "第二个参数为 $2"
  	echo "第四个参数为 $4"
  	echo "总参数为$#"
  	echo "作为一个字符串输出所有参数 $*"
  }
  
  [root@basenode1 ~]# sh test.sh
  第一个参数为 1
  第二个参数为 2
  第四个参数为 4
  总参数为9
  作为一个字符串输出所有参数 1 2 3 4 5 6 7 8 9
  ```

  

## 4. 系统任务设置

### 4.1 系统启动流程

- 启动计算机的硬件(BIOS)
  - 读取时间
  - 选择对应的启动模式(`USB HDD EFI`)

- 如果是Linux系统，回去找**/boot**目录，引导这个系统启动

- 计算机系统开始启动，读取初始化配置文件

  ```sh
  [root@basenode1 ~]# vi /etc/inittab 
  # inittab is no longer used when using systemd.
  #
  # ADDING CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.
  #
  # Ctrl-Alt-Delete is handled by /usr/lib/systemd/system/ctrl-alt-del.target
  #
  # systemd uses 'targets' instead of runlevels. By default, there are two main targets:
  #
  # multi-user.target: analogous to runlevel 3
  # graphical.target: analogous to runlevel 5
  #
  # To view current default target, run:
  # systemctl get-default
  #
  # To set a default target, run:
  # systemctl set-default TARGET.target
  #
  ```

  - 启动时控制着计算机的运行级别`runlevel`

  - | *0*   | **halt关机**                                                 |
    | ----- | ------------------------------------------------------------ |
    | **1** | **Single User Mode(单用户模式)**                             |
    | **2** | **Multiuser,without NFS（多用户模式，但是无网络状态）`FS--->FileSystem`** |
    | **3** | **Full Multiuser mode（多用户完整版模式）**                  |
    | **4** | **unused（保留模式）**                                       |
    | **5** | **`X11`（用户界面模式）**                                    |
    | **6** | **reboot（重启模式）**                                       |

  - id:3:默认runlevel为3

  - 以runlevel=3开始启动对应的服务和组件

- 开始默认引导公共的组件或者服务

  ```sh
  [root@basenode1 rc3.d]# ll
  total 0
  lrwxrwxrwx. 1 root root 20 Aug 23 00:39 K50netconsole -> ../init.d/netconsole
  lrwxrwxrwx. 1 root root 17 Aug 23 00:39 S10network -> ../init.d/network
  lrwxrwxrwx  1 root root 15 Aug 29 13:30 S95jexec -> ../init.d/jexec
  ```

  - K:关机时需要关闭的服务
  - S：启动时需要启动的服务
  - 数字代表了开启或关闭的顺序
  - 所有的文件都是软链接，链接的地址为`/etc/init.d`

- 启动完毕后，所有的服务也被加载完成



### 4.2 系统服务

- 我们可以使用chkconfig命令查看当前虚拟机的服务
- 通过查看可以得知不同级别对应到每一个服务确定本次开机自动启动
- 开机结束后，我们需要使用systemctl命令控制服务的开启或者关闭



### 4.3 开机自动启动服务

- rc.local

  - 首先创建脚本存放的文件夹

    ```sh
    mkdir -p /usr/local/scripts
    ```

  - 在文件夹中创建脚本文件

    ```sh
    vi scripts.sh
    ------------------------------------------
    #! /bin/bash
    yum info ntp && ntpdate cn.otp.org.cn
    
    ## 給予执行权限
    ```

  - 去 /etc/rc.d/rc.local文件夹中添加脚本的绝对路径

    - 给予`rc.local`执行权限

- ```sh
  [root@basenode1 rc.d]# date
  Thu Sep  1 15:08:31 CST 2022
  [root@basenode1 rc.d]# date -s  '21:21:21'
  Thu Sep  1 21:21:21 CST 2022
  [root@basenode1 rc.d]# reboot
  Connection closing...Socket close.
  
  Connection closed by foreign host.
  
  Disconnected from remote host(basenode1) at 15:09:17.
  
  Type `help' to learn how to use Xshell prompt.
  [C:\~]$ 
  
  Connecting to 192.168.88.110:22...
  Connection established.
  To escape to local shell, press 'Ctrl+Alt+]'.
  
  WARNING! The remote SSH server rejected X11 forwarding request.
  Last login: Thu Sep  1 15:03:00 2022 from 192.168.88.1
  [root@basenode1 ~]# date
  Thu Sep  1 15:09:58 CST 2022
  ```

  可以看到，我添加一个开机自动校验时间的脚本，然后修改时间，重启电脑之后，发现时间恢复正常

- chkconfig

  - 创建开机自启动脚本文件

  - vi script.sh

    ```bash
    /! /bin/bash
    #chkconfig: 2345 88 99
    #description:auto_run
    
    #开机自动同步时间
    yum info ntp && ntpdate cn.otp.org.cn
    ```

  - 设置执行权限

    ```
    chmod u+x script.sh
    ```

  - 将脚本拷贝到/etc/init.d目录下

    ```sh
    cp script.sh /etc/init.d
    ```

  - **添加到服务**

    ```sh
    chkconfig --add /etc/init.d/script.sh 
    ```

  - 重启

    ```sh
    reboot
    ```



### 4.4 定时服务

- 在系统服务中心，crond负责周期任务

  - **`systemctl status crond.service`**

    ```sh
    [root@basenode1 ~]# systemctl status crond.service
    ● crond.service - Command Scheduler
       Loaded: loaded (/usr/lib/systemd/system/crond.service; enabled; vendor preset: enabled)
       Active: active (running) since Thu 2022-09-01 15:17:43 CST; 20min ago
     Main PID: 766 (crond)
       CGroup: /system.slice/crond.service
               └─766 /usr/sbin/crond -n
    
    Sep 01 15:17:43 basenode1 systemd[1]: Started Command Scheduler.
    Sep 01 15:17:43 basenode1 crond[766]: (CRON) INFO (RANDOM_DELAY will be scaled with factor 66% if used.)
    Sep 01 15:17:43 basenode1 crond[766]: (CRON) INFO (running with inotify support)
    ```

  - 添加任务，编辑当前用户的任务列表

    ```sh
    [root@basenode1 ~]# crontab -e
    no crontab for root - using an empty one
    crontab: no changes made to cronta
    ```

- **编辑任务**

  **分 时 日 月 周 命令**

  ```sh
  30 21 * * * /usr/local/etc/rc.d/lighttpd restart
  #表示每晚的21.30重启apache
  
  45 4 1,10,22 * * /usr/local/etc/rc.d/lighttpd restart
  #表示每月的1,10,22号的4:45重启apache
  
  0,30 18-23 * * * /usr/local/etc/rc.d/lighttpd restart
  #表示每天18.00-23.00之间每隔30分钟重启apache
  
  ```

- 重启crontab,使配置生效

  ```sh
  systemctl restart crond.service
  ```

- **查看当前的定时任务**

  ```sh
  crontab -l
  ```

- **查看历史任务**

  ```sh
  cat /var/spool/mail/root
  ```

- **清除任务**

  ```sh
  crontab -r
  ```

  
