# stat命令 #

## 命令格式 ##

> stat [文件或目录]

## 命令功能及介绍 ##

显示文件或目录的详细信息，也显示inode内容

## 命令参数 ##

    -f　　不显示文件本身的信息，显示文件所在文件系统的信息
    -L　　显示符号链接
    -t　　简洁模式，只显示摘要信息

## 例子和技巧 ##

### 查询文件的inode信息 ###

```
[root@server link-study]# ls
file  folder  hard.link1  hard.link2  soft.link
[root@server link-study]# stat file
  File: `file'
  Size: 45        	Blocks: 8          IO Block: 4096   regular file
Device: fd00h/64768d	Inode: 395902      Links: 3
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2016-08-31 17:23:37.178074219 +0800
Modify: 2016-08-31 17:25:13.167078607 +0800
Change: 2016-08-31 17:25:13.169078555 +0800
```

显示信息：

1. 第一行：File：文件名
2. 第二行：
    - Size：文件字节数
    - Blocks：
