# 磁盘分区 #

## MBR 主引导扇区 ##

> 主引导扇区位于整个硬盘的0磁头0柱面1扇区，包括硬盘主引导记录MBR（Master Boot Record）和分区表DPT（Disk Partition Table），以及最后结束标志。

MBR一般共512字节，从磁盘的0磁头0柱面1扇区开始，前446字节是引导程序，接着的64字节是分区表，最后2字节是结束标志。

### 引导代码 ###
计算机在上电完成BIOS自检后，会将该主引导扇区加载到内存中并执行前面446字节的引导程序，引导程序首先会在分区表中查找活动分区，若存在活动分区，则根据活动分区的偏移量找到该活动分区上的引导扇区的地址，并将该引导扇区加载到内存中，同时检查该引导扇区的有效性，然后根据该引导扇区的规则去引导操作系统。在一些非启动磁盘上，MBR引导代码可能都是0，这对磁盘使用没有任何影响。

### 分区表 ###
通过分区表信息来定位各个分区，访问用户数据。

分区表包含4个分区项，每一个分区项通过位置偏移、分区大小来唯一确定一个主分区或者扩展分区。每个分区项占16字节，包括引导标识、起始和结束位置的CHS参数、分区类型、开始扇区、分区大小等。

### 结束标志 ###
结束标志是固定的“55 AA”，占2个字节。

每次执行系统引导代码时都会检查MBR主引导扇区最后2字节是否是"55 AA"，若是，则继续执行后续的程序，否则，则认为这是一个无效的MBR引导扇区，停止引导系统。


# Linux分区命名 #

分区类型常见的有：主分区、扩展分区、逻辑分区

主引导分扇区的分区表共64字节，一个分区的信息需要16字节，这样一块磁盘最多只能有4个分区，这样直接注册在分区表上的分区都是**主分区**。

明显4个分区是不够的，所以有了**扩展分区**。扩展分区也是主分区，但扩展分区中可以在建立新的分区，在扩展分区中新建的分区就是**逻辑分区**。逻辑分区不受分区表大小限制。


## 命名 ##
Linux中会把磁盘和磁盘分区以文件的方式存储在/dev下。

不同类型的硬盘和分区的设备文件有统一的命名规则：

硬盘：

| 硬盘接口类型      | 命名规则     |
| :------------ | :----------- |
| IDE接口       | hdX      |
| STAT或SCSI接口     |  sdX      |
X表示a、b、c、d等，不同接口类型的X统一计数。如：第一块是IDE接口的硬盘，第二块是STAT接口的硬盘，则/dev中的硬盘文件为hda和sdb。

分区：

在硬盘命名的基础后加数字即可，数字统一计数。如：hda1,hda2,sdb3,sdb4,sdb5

另外：

所有的USB接口接入的移动存储设备，移动硬盘、U盘、USB光驱都使用sdXY命名；光驱（光盘设备）命名与接口无关，都是cdrom


# LVM扩容技术 #
...
