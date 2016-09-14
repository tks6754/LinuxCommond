# tail命令 #

## 命令格式 ##
> tail [必要参数][可选参数] [文件]  

## 命令功能及介绍 ##

将指定文件写入到标准输出，显示末尾内容；不指定文件时，作为输入信息进行处理。

## 命令参数 ##

    -f 循环读取
    -q 不显示处理信息
    -v 显示详细的处理信息
    -c<数目> 显示的字节数
    -n<行数> 显示行数
    --pid=PID 与-f合用,表示在进程ID,PID死掉之后结束.
    -q, --quiet, --silent 从不输出给出文件名的首部
    -s, --sleep-interval=S 与-f合用,表示在每次反复的间隔休眠S秒

## 例子和技巧 ##

### 显示从倒数第n行内容 ###

    tail -n 5 log.log

### 从正数第n行开始显示内容 ###
    tail -n +5 log.log


### 循环查看内容 ###

    tail -f log.log

不断的ping远程机器，并将结果输出到test.log,Ctrl+c来结束，然后查看test.log

    ping 192.168.120.220 > test.log & tail -f test.log
