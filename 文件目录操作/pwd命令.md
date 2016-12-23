# pwd命令 #

## 命令格式 ##
>pwd [参数]

## 命令功能及介绍 ##
查看当前目录的路径

## 命令参数 ##
    -P 输出物理路径。如果目录是链接时，显示实际路径，而非使用链接（link）路径
    -L 目录连接链接时，输出连接路径

## 例子和技巧 ##

### 查看当前工作目录的完整路径 ###
    pwd

### 目录连接链接时，pwd -P  显示出实际路径，而非使用连接（link）路径；pwd显示的是连接路径 ###
    [root@localhost soft]# cd /etc/init.d
    [root@localhost init.d]# pwd
    /etc/init.d
    [root@localhost init.d]# pwd -P
    /etc/rc.d/init.d
    [root@localhost init.d]#

### /bin/pwd [选项] 选项：-L 目录连接链接时，输出连接路径 -P 输出物理路径 ###
    [root@localhost init.d]# /bin/pwd
    /etc/rc.d/init.d
    [root@localhost init.d]# /bin/pwd --help
    [root@localhost init.d]# /bin/pwd -P
    /etc/rc.d/init.d
    [root@localhost init.d]# /bin/pwd -L
    /etc/init.d
    [root@localhost init.d]#
