**安装ansible**

```
# yum install -y ansible
```

**查看ansible版本和安装位置**
```
[root@localhost ~]# ansible --version
ansible 2.9.27
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.5 (default, Jun 28 2022, 15:30:04) [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)]
```


**主机清单配置文件**
```
# vi /etc/ansible/hosts

[web]
10.240.207.123
10.240.207.124

[nfs]
10.240.207.128
```

**主机分组后，执行测试**
```
# ansible all -m shell -a "hostname" 
The authenticity of host '10.240.207.123 (10.240.207.123)' can't be established.
ECDSA key fingerprint is SHA256:v5JuLp0dC8QHMbtI7HcfAijNEYc/KrOvLIIuq2+2QQ0.
ECDSA key fingerprint is MD5:34:ee:33:56:c7:d8:84:d7:d1:75:e8:02:68:24:d6:60.
Are you sure you want to continue connecting (yes/no)? The authenticity of host '10.240.207.124 (10.240.207.124)' can't be established.
ECDSA key fingerprint is SHA256:v5JuLp0dC8QHMbtI7HcfAijNEYc/KrOvLIIuq2+2QQ0.
ECDSA key fingerprint is MD5:34:ee:33:56:c7:d8:84:d7:d1:75:e8:02:68:24:d6:60.
Are you sure you want to continue connecting (yes/no)? The authenticity of host '10.240.207.128 (10.240.207.128)' can't be established.
ECDSA key fingerprint is SHA256:v5JuLp0dC8QHMbtI7HcfAijNEYc/KrOvLIIuq2+2QQ0.
ECDSA key fingerprint is MD5:34:ee:33:56:c7:d8:84:d7:d1:75:e8:02:68:24:d6:60.
Are you sure you want to continue connecting (yes/no)? yes 
10.240.207.123 | UNREACHABLE! => {
    "changed": false, 
    "msg": "Failed to connect to the host via ssh: Could not create directory '/root/.ssh'.\r\nWarning: Permanently added '10.240.207.123' (ECDSA) to the list of known hosts.\r\nPermission denied (publickey,gssapi-keyex,gssapi-with-mic,password).", 
    "unreachable": true
}

10.240.207.124 | UNREACHABLE! => {
    "changed": false, 
    "msg": "Failed to connect to the host via ssh: Host key verification failed.", 
    "unreachable": true
}

10.240.207.128 | UNREACHABLE! => {
    "changed": false, 
    "msg": "Failed to connect to the host via ssh: Could not create directory '/root/.ssh'.\r\nHost key verification failed.", 
    "unreachable": true
}
```
无法连接到目标机器

**Ansible批量管理主机有两种方式**

- 传统密码认证

- 公钥认证

**Ansible基于公私钥认证**

1. 将master机器的公钥分发给需要免密登录的机器
```
# ssh-copy-id root@10.240.207.128
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
The authenticity of host '10.240.207.128 (10.240.207.128)' can't be established.
ECDSA key fingerprint is SHA256:v5JuLp0dC8QHMbtI7HcfAijNEYc/KrOvLIIuq2+2QQ0.
ECDSA key fingerprint is MD5:34:ee:33:56:c7:d8:84:d7:d1:75:e8:02:68:24:d6:60.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@10.240.207.128's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'root@10.240.207.128'"
and check to make sure that only the key(s) you wanted were added.
```

2. 后续操作可以免密执行
```
[root@localhost ~]# ansible all -m shell -a "hostname" 
10.240.207.128 | CHANGED | rc=0 >>
localhost.localdomain
10.240.207.123 | CHANGED | rc=0 >>
localhost.localdomain
10.240.207.124 | CHANGED | rc=0 >>
localhost.localdomain
```


**关于Ansible指纹确认的问题**

master需要确认目标机器的指纹,记录到本地known_hosts文件

```
[root@localhost ~]# ls ~/.ssh/known_hosts
/root/.ssh/known_hosts
```
这里存放的目标机器的指纹信息


## Ansible命令执行方式
```
[root@localhost ~]# ansible-doc -l|wc -l
3387
```
当前Ansible支持3387个模块

Ansible实现批量主机管理的模式主要有两个

- 利用ansible命令实现批量管理(ad-hoc模式)

- 利用ansible剧本实现批量管理(playbook模式)


## Ansible核心内容

**Ansible命令执行结果（状态颜色）**

    绿色：命令以用户的期望执行了，但是状态没有发生改变

    黄色：命令以用户的期望执行了，状态发生了改变

    紫色：警告信息，说明ansible提示你有更合适的用法

    红色：命令错误，执行失败

    蓝色：详细的执行过程    


### ping测试连通性

```
[root@localhost ~]# ansible all -m ping
10.240.207.128 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
10.240.207.124 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
10.240.207.123 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
```
 
### command简单命令模块

语法，查看提示
```
[root@localhost ~]# ansible-doc -s command
- name: Execute commands on targets
  command:
      argv:                  # Passes the command as a list rather than a string.
                               Use `argv' to avoid
                               quoting values that
                               would otherwise be
                               interpreted
                               incorrectly (for
                               example "user
                               name"). Only the
                               string or the list
                               form can be
                               provided, not both.
                               One or the other
                               must be provided.
      chdir:                 # Change into this directory before running the
                               command.
      cmd:                   # The command to run.
      creates:               # A filename or (since 2.0) glob pattern. If it
                               already exists, this
                               step *won't* be run.
      free_form:             # The command module takes a free form command to
                               run. There is no
                               actual parameter
                               named 'free form'.
      removes:               # A filename or (since 2.0) glob pattern. If it
                               already exists, this
                               step *will* be run.
      stdin:                 # Set the stdin of the command directly to the
                               specified value.
      stdin_add_newline:     # If set to `yes', append a newline to stdin data.
      strip_empty_ends:      # Strip empty lines from the end of stdout/stderr in
                               result.
      warn:                  # Enable or disable task warnings.
 ```
 该模块的作用：在远程节点上执行一个命令

 command模块是ansible命令基本模块
 
 - 使用command模块执行远程命令，命令不得用变量（$HOME）
 - 不得出现特殊符号
 - 也就是无法使用复杂的linux命令，需要通过shell模块来实现

 **远程查看主机名**

 ```
 [root@localhost ~]# ansible all -a "hostname"
10.240.207.124 | CHANGED | rc=0 >>
localhost.localdomain
10.240.207.128 | CHANGED | rc=0 >>
localhost.localdomain
10.240.207.123 | CHANGED | rc=0 >>
localhost.localdomain
 ```

**远程查看内存信息**
```
[root@localhost ~]# ansible web -a "free -m"
10.240.207.123 | CHANGED | rc=0 >>
              total        used        free      shared  buff/cache   available
Mem:           7820         287        7318           8         214        7293
Swap:          1955           0        1955
10.240.207.124 | CHANGED | rc=0 >>
              total        used        free      shared  buff/cache   available
Mem:           7820         275        7404           8         140        7336
Swap:          1955           0        1955
```

**远程创建文件查看文件**

创建
```
[root@localhost ~]# ansible nfs -a "touch /opt/tmp.log"
[WARNING]: Consider using the file module with state=touch rather than running
'touch'.  If you need to use command because file is insufficient you can add
'warn: false' to this command task or set 'command_warnings=False' in ansible.cfg
to get rid of this message.
10.240.207.128 | CHANGED | rc=0 >>
```

查看
```
[root@localhost ~]# ansible nfs -a "cat /opt/tmp.log"
10.240.207.128 | CHANGED | rc=0 >>
```


**远程获取机器负载**
```
[root@localhost ~]# ansible all  -a "uptime"
10.240.207.128 | CHANGED | rc=0 >>
 17:50:09 up  4:31,  3 users,  load average: 0.00, 0.01, 0.04
10.240.207.123 | CHANGED | rc=0 >>
 17:50:09 up  6:37,  3 users,  load average: 0.00, 0.01, 0.05
10.240.207.124 | CHANGED | rc=0 >>
 17:50:09 up  4:40,  3 users,  load average: 0.00, 0.01, 0.04
```

**关闭告警信息**

追加 warn=false
```
[root@localhost ~]# ansible nfs -a "touch /opt/tmp.log warn=false"
10.240.207.128 | CHANGED | rc=0 >>
```

**远程创建用户**
```
[root@localhost ~]# ansible nfs -a "useradd loca"
10.240.207.128 | CHANGED | rc=0 >>

[root@localhost ~]# ansible all -a "useradd loca"
10.240.207.128 | FAILED | rc=9 >>
useradd：用户“loca”已存在non-zero return code
10.240.207.123 | CHANGED | rc=0 >>

10.240.207.124 | CHANGED | rc=0 >>

```
|  选项参数   | 选项说明  |
|  ----       | ----     |
| chdir      | 在执行命令，通过cd命令进入指定目录               |
| creates      |    定义一个文件是否存在，若不存在则运行相应命令；存在则跳过 |
|free_form(必须) |参数信息中可以输入任何系统命令，实现远程管理 |
|removes|定义一个文件是否存在，如果存在则运行相应命令；如果不存在则跳过|



# PlayBook
Playbook采用一种可读性很高的且容易被人类阅读的语法的YAML语法编写，YAML: "YAML Ain't a Markup Language"（YAML不是一种置标语言）。该语言在被开发时，YAML 的意思其实是："Yet Another Markup Language"（仍是一种置标语言），格式如下所示：

```yaml
house:
  family:
    name: Doe
    parents:
      - John
      - Jane
    children:
      - Paul
      - Mark
      - Simone
  address:
    number: 34
    street: Main Street
    city: Nowheretown
  zipcode: 12345
```

## 1.2 YAML简介

### 1.2.1 YAML特性

1. YAML的可读性好
2. YAML和脚本语言的交互性好
3. YAML使用实现语言的数据类型
4. YAML有一个一致的信息模型
5. YAML易于实现

### 1.2.2 YAML语法

1. YAML使用可打印的Unicode字符，可使用UTF-8或UTF-16。
2. 使用空白字符未文件缩排来表示结构；不过不能使用跳格字符。
3. 注解由井字号( # )开始，可以出现在一行中的任何位置，而且范围只有一行(也就是一般所谓的单行注解)
4. 每个清单成员以单行表示，并用短杠+空白( - )起始。或使用方括号( [ ] )，并用逗号+空白( , )分开成员。
5. 每个杂凑表的成员用冒号+空白( : )分开键值和内容。或使用大括号( { } )，并用逗号+空白( , )分开。 杂凑表的键值可以用问号 ( ? )起始，用来明确的表示多个词汇组成的键值。
6. 字串平常并不使用引号，但必要的时候可以用双引号 ( " )或单引号 ( ' )框住。使用双引号表示字串时，可用倒斜线( \ )开始的跳脱字符(这跟C语言类似)表示特殊字符。
7. 区块的字串用缩排和修饰词(非必要)来和其他资料分隔，有新行保留(preserve)(使用符号 | )或新行折叠(flod)(使用符号 > )两种方式。
8. 在单一档案中，可用连续三个连字号(——)区分多个档案。另外，还有选择性的连续三个点号( ... )用来表示档案结尾。
9. 重复的内容可使从参考标记星号 ( * )复制到锚点标记( & )。
10. 指定格式可以使用两个惊叹号 ( !! )，后面接上名称。
11. 档案中的单一文件可以使用指导指令，使用方法是百分比符号( % )。有两个指导指令

# PlayBook实战
playbook将会使Ansible成为超一流的管理工具。

## 2.1 Shell脚本与Playbook的转换

现在越来越多的DevOPS也开始将目光移向了Ansible，因为Ansible可以轻松的将shell脚本或简单的shell命令转换为Ansible plays.

下面有一个安装apache的shell脚本：
```shell
#!/bin/bash
# 安装Apache
yum install --quiet -y httpd httpd-devel
# 复制配置文件
cp /path/to/config/httpd.conf /etc/httpd/conf/httpd.conf
cp /path/to/httpd-vhosts.conf /etc/httpd/conf/httpd-vhosts.conf
# 启动Apache，并设置开机启动
service httpd start
chkconfig httpd on
```
将其转换为一个完整的playbook后：

```yaml
---
- hosts: localhost

  tasks:
   - name: "安装Apache"
     command: yum install --quiet -y httpd httpd-devel
   - name: "复制配置文件"
     command: cp /tmp/httpd.conf /etc/httpd/conf/httpd.conf
     command: cp /tmp/httpd-vhosts.conf /etc/httpd/conf/httpd-vhosts.conf
   - name: "启动Apache，并设置开机启动"
     command: service httpd start
     command: chkconfig httpd on
```
在上述playbook中，我们使用了“command”模块来运行了标准的shell命令。我们还给了每一出play一个“name”，因此当我们运行playbook时，每一个play都会有非常易读的的信息输出：
```bash
[root@master tmp]# ansible-playbook ./playbook.yml
[WARNING]: While constructing a mapping from /root/Desktop/tmp/playbook.yml, line 7, column 6, found a
duplicate dict key (command). Using last defined value only.
[WARNING]: While constructing a mapping from /root/Desktop/tmp/playbook.yml, line 10, column 6, found
a duplicate dict key (command). Using last defined value only.

PLAY [localhost] **************************************************************************************
TASK [Gathering Facts] ********************************************************************************ok: [localhost]

TASK [安装Apache] ***************************************************************************************
[WARNING]: Consider using the yum module rather than running 'yum'.  If you need to use command
because yum is insufficient you can add 'warn: false' to this command task or set
'command_warnings=False' in ansible.cfg to get rid of this message.
changed: [localhost]

TASK [复制配置文件] *****************************************************************************************
fatal: [localhost]: FAILED! => {"changed": true, "cmd": ["cp", "/tmp/httpd-vhosts.conf", "/etc/httpd/conf/httpd-vhosts.conf"], "delta": "0:00:00.004822", "end": "2023-08-07 16:24:25.530414", "msg": "non-zero return code", "rc": 1, "start": "2023-08-07 16:24:25.525592", "stderr": "cp: cannot stat ‘/tmp/httpd-vhosts.conf’: No such file or directory", "stderr_lines": ["cp: cannot stat ‘/tmp/httpd-vhosts.conf’: No such file or directory"], "stdout": "", "stdout_lines": []}

PLAY RECAP ********************************************************************************************localhost                  : ok=2    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0 
```

## 2.2 Playbook案例逐行剖析

1. 第一行，“---”，这个是YAML语法中注释的用法，就像shell脚本中的“#”号一样
2. 第二行，“- hosts: all”，告诉ansible具体要在哪些主机上运行我的剧本（playbook），在本例中是localhsot，即本机
3. 第三行，“sudo: yes”，告诉ansible通过sudo来运行相应命令，这样所有命令将会以root身份执行
4. 第四行，“tasks:”，指定一系列将要运行的任务

> 每一个任务（play）以“- name: 安装Apache”开头。“- name:”字段并不是一个模块，不会执行任务实质性的操作，它只是给“task” 一个易于识别和名称。即便把name字段对应的行完全删除，也不会有任何问题。
本例中我们使用yum模块来安装Apache，替代了“yum -y install httpd httpd-devel”

>在每一个play当中，都可以例用 with_items 来定义变量，并通过“{{ 变量名 }}”的形式来直接使用使用yum模块的state=present选项来确保软件被安装，或者使用state=absent来确保软件被删除

>第二个任务（play）同样是“- name”字符开头

>我们使用copy模块来将“src”定义的源文件（必须是ansible所在服务器上的本地文件 ）复制到“dest”定义的目的地址（此地址为远程主机的上地址）去,在传递文件的同时，还定义了文件的属主，属组和权限

>这个play中，我们用数组的形式给变量赋值，使用{var1: value, var2: value} 的格式来赋值，变量的个数可以任意多，不同变量间以逗号分隔，使用{{item.var1 }}的形式来调用变量，本例中为：{{ item.src }}


5. 第三个任务（play）使用了同样的结构，调用了service模块，以保证服务的正常开启

## 2.3 Playbook与Shell脚本差异对比

当我们把shell脚本转换为playbook运行的时候，ansible会留下清晰的执行痕迹，明确告诉我们在每一台主机上的每一步都做了什么。

更厉害的是，当我们重复执行一个playbook时，当ansible发现系统的现有状态符合playbook所定义的状态时，anbile将自动跳过该操作。

比如下图，我们再次执行playbook: temp.yml，当ansible发现playbook中的play都已被完成，它将直接返回ok状态码，速度非常之快。
如果是shell脚本，肯定会硬着头皮，把所用操作再做一遍。

在正式运行playbook之前，可以使用--check 或 -C 选项来检测playbook都会改变哪些内容，显示的结果跟真正执行时一模一样，但不会真的对被管理的服务器产生影响


# 3. Ansible-playbook命令详解

## 3.1 限定执行范围

```
--limit   
```

如果我们运行上面的例子，会发现所有被ansible管理的主机都会被操作。
我们可以通过修改“- hosts：”字段来指定哪些主机将会应用playbook的操作，

指定一台主机：10.240.207.123
指定多台主机：10.240.207.123,10.240.207.124
指定一组主机：web

当然，也可以直接通过ansible-playbook命令来指定主机：
```bash
# ansible-playbook playbook.yml --limit webservers
```
这样（假设你的inventory文件中包含webserver组），即便playbook中设定“hosts: all”，但也仅对webserver组生效。

```bash
--list-hosts
```
如果想知道在执行playbook时，哪些主机将会受影响，则使用--list-hosts选项：
```bash
# ansible-playbook playbook.yml --list-hosts 
```

# 4. Ansible-playbook: 用户与权限设置

Playbook中，如果在与hosts同组的字段中没有定义user，那么Ansible将会使用你在inventory文件中定义的用户，如里inventory文件中也没定义用户，Ansible将默认使用当前系统用户身份来通过SSH连接远程主机，在运程程主机中运行play内容。

我们也可以直接在ansible-playbook中使用 --remote-user选项来指定用户：
```bash
# ansible-playbook playbook.yml --remote-user=tom
```
在某些情况下，我们需要传递sudo密码到远程主机，来保证sudo命令的正常运行。这时，可以使用--ask-sudo-pass (-K)选项来交互式的输入密码。

使用--sudo选项，可以强制所有play都使用sudo用户，同时使用--sudo-user选项指定切换到具体哪个用户，如果不指定，则默认以root身份运行。

比如，当前用户Tom想以Jerry的身份运行playbook，命令如下：
$ ansible-playbook playbook.yml --sudo --sudo-user=jerry --ask-sudo-pass
执行过程中，会要求用户输入Jerry的密码。


# 5.Ansible-playbook: 其它选项

Ansible-playbook命令还有一些其他选项：

```
--inventory=PATH (-i PATH)：指定inventory文件，默认文件是/etc/ansible/hosts

--verbose(-v)：显示详细输出，也可以使用-vvvv显示精确到每分钟的输出

--extra-vars=VARS(-e VARS)：定义在playbook使用的变量，格式为："key=value,key=value"

--forks=NUM ( -f NUM)：指定并发执行的任务数，默认为5，根据服务器性能，调大这个值可提高ansible执行效率

--connection=TYPE ( -c TYPE)：指定连接远程主机的方式，默认为ssh，设为local时，刚只在本地执行playbook，建议不做修改

--check：检测模式，playbook中定义的所有任务将在每台远程主机上进行检测，但并不直正执行
```
