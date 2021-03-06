# ln命令 #

## 命令格式 ##
> ln [参数] [源文件或目录] [目标文件或目录]

## 命令功能及介绍 ##

建立文件或目录链接（硬链接、软连接）

## 命令参数 ##

**必要参数**

    -b 删除，覆盖以前建立的链接
    -d 允许超级用户制作目录的硬链接
    -f 强制执行
    -i 交互模式，文件存在则提示用户是否覆盖
    -n 把符号链接视为一般目录
    -s 软链接(符号链接)
    -v 显示详细的处理过程

**可选参数**

    -S “-S<字尾备份字符串> ”或 “--suffix=<字尾备份字符串>”
    -V “-V<备份方式>”或“--version-control=<备份方式>”
    --help 显示帮助信息
    --version 显示版本信息

## 例子和技巧 ##

### 给文件建立软连接 ###

ln -s file soft.link

### 给文件建立硬链接 ###

ln file hard.link

## 补充 ##

### inode ###

![inode](https://github.com/tks6754/Photos01/raw/master/inode.jpg)

在文件系统中，对一个硬盘分区、格式化后，每个分区被分割为两个部分：Inode区域和数据区域。Inode区域存储元数据，inode是 一个文件在文件系统中的唯一标识，访问文件必须先找到并读取这个文件的inode。

inode中保存了：唯一标识Inumber、创建时间（ctime）、修改时间(mtime) 、文件大小、属主、归属的用户组、读写权限、数据所在block号等信息。

读取文件的方式

![file-inode](https://github.com/tks6754/Photos01/raw/master/file-inode.jpg)



### 链接 ###

Linux中链接有两种，硬链接（Hard Link）和符号链接（Symbolic Link，也称软链接）。

一幅很常见的图

![link](https://github.com/tks6754/Photos01/raw/master/linux-link.jpg)

**硬链接**

硬链接可以看成是一个“filename”，它“指向”的inode内容是完全相同的。相当于一个inode有多个“filename”，再根据inode找到数据块。所以，删除一个硬链接是不会删除数据块，只有删除一个数据块的最后一个硬链接才会删除数据块。

- 硬链接是有着相同 inode 号仅文件名不同的文件，增加文件硬链接不会占用存储空间。
- 只能对文件进行创建，文件夹不可以。
- 硬链接只能在同一个文件系统中创建。

**软链接**

软链接是类似于Win下的快捷方式的概念，它是一个特殊的文本文件，文件内容是另一个文件的位置信息。所以，删除一个文件的所有软链接不会导致文件被删除，但原文件移动或删除，会导致软链接找不到文件，处于失效状态。

- 软链接占用存储空间
- 可以对文件以及文件夹创建
- 软链接没有文件系统的限制，甚至可以跨系统建立


```
[root@server link-study]# ls -li
total 4
395902 -rw-r--r--. 3 root root    0 Aug 31 12:15 file
395903 drwxr-xr-x. 2 root root 4096 Aug 31 12:15 folder
395902 -rw-r--r--. 3 root root    0 Aug 31 12:15 hard.link1
395902 -rw-r--r--. 3 root root    0 Aug 31 12:15 hard.link2
395904 lrwxrwxrwx. 1 root root    4 Aug 31 12:16 soft.link -> file
[root@server link-study]# stat file
  File: `file'
  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: fd00h/64768d	Inode: 395902      Links: 3
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2016-08-31 12:15:50.188096551 +0800
Modify: 2016-08-31 12:15:50.188096551 +0800
Change: 2016-08-31 12:16:16.341094815 +0800
[root@server link-study]# stat hard.link1
  File: `hard.link1'
  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: fd00h/64768d	Inode: 395902      Links: 3
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2016-08-31 12:15:50.188096551 +0800
Modify: 2016-08-31 12:15:50.188096551 +0800
Change: 2016-08-31 12:16:16.341094815 +0800
```
