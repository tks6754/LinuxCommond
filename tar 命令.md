# tar命令 #

## 命令格式 ##
> tar [必要参数][可选参数] [文件]

## 命令功能及介绍 ##
压缩、解压缩、打包、解包

    打包和压缩
    打包是将一大堆文件或目录变成一个总的文件；压缩将一个大的文件通过压缩算法变成一个小的文件。

    Linux中，很多压缩只针对单个文件进行压缩，当有多个文件或目录时，先打成一个包（tar命令），然后再进行压缩（gzip bzip2等命令）

    tar命令本身不具有压缩功能，但它会调用压缩功能实现压缩。

## 命令参数 ##

**必要参数 **

    -A 新增压缩文件到已存在的压缩
    -B 设置区块大小
    -c 建立新的压缩文件
    -d 记录文件的差别
    -r 添加文件到已经压缩的文件
    -u 添加改变了和现有的文件到已经存在的压缩文件
    -x 从压缩的文件中提取文件
    -t 显示压缩文件的内容
    -z 支持gzip解压文件
    -j 支持bzip2解压文件
    -Z 支持compress解压文件
    -v 显示操作过程
    -l 文件系统边界设置
    -k 保留原有文件不覆盖
    -m 保留文件不被覆盖
    -W 确认压缩文件的正确性

**可选参数**

    -b 设置区块数目
    -C 切换到指定目录
    -f 指定压缩文件
    --help 显示帮助信息
    --version 显示版本信息

## 例子和技巧 ##

### 打包、压缩文件 ###

仅打包，不压缩

      tar -cvf log.tar logtest.log

打包后，用gzip压缩

      tar -zcvf log.tar.gz logtest.log

打包后，用bzip2压缩

      tar -jcvf log.tar.bz2 logtest.log

参数c建立新的压缩文件。

参数 f 后的文件名是自己取的，用于指定打包后的文件名。

习惯用 **.tar** 标识打包后的文件；用 **.tar.gz** 或 **.tgz** 表示加参数z，将打包后文件又用gzip压缩后的文件；用 **.tar.bz2** 标识加参数j，将打包文件又用bzip2压缩后的文件。

### 查看包中的文件 ###

    tar -ztvf log.tar.gz

参数t显示压缩文件内容，由于包使用了gzip压缩，查看是需要指定参数z。

### 解压缩 ###

    tar -zxvf /opt/soft/test/log.tar.gz

参数x从包中提取文件，可以将文件提取到当前目录（命令执行目录）下。

### 解压部分目录 ###

压缩两个文件

    tar -czvf log12.tar.gz log1.log log2.log

解压出log1.log

    tar -czvf log12.tar.gz log1.log log2.log

### 压缩并保留其权限属性 ###

    tar -czvpf log12.tar.gz log1.log log2.log
    tar -xzvpf log12.tar.gz

参数 p保留压缩文件的属性，解压后权限与压缩前相同。

### 对超过某时间点后的文件进行压缩 ###

    tar -N "2012/11/13" -zcvf log17.tar.gz test

### 排除某些文件进行压缩 ###

    [root@localhost test]# tree scf
    scf
    |-- bin
    |-- doc
    |-- lib
    `-- service
       	 `-- deploy
           	 	|-- info
           	 	`-- product
    7 directories, 0 files
    [root@localhost test]# tar --exclude scf/service -zcvf scf.tar.gz scf/*
    scf/bin/
    scf/doc/
    scf/lib/
    [root@localhost test]#

使用exclude排除某些文件。
