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

**Command练习**

备份/var/log日志目录 需要先进入根目录
