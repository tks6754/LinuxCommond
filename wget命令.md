# wget命令 #

## 命令格式 ##
> rm [参数] [URL地址]

## 命令功能及介绍 ##
wget是一个文件下载工具，支持http、https、ftp协议，可是使用http代理；

支持自动下载，用户启动一个下载任务后，用户退出，任务可以继续进行；

没有指定下载路径时，默认为当前路径


## 命令参数 ##

### 启动参数 ###

    -V, –version 显示wget的版本后退出
    -h, –help 打印语法帮助
    -b, –background 启动后转入后台执行
    -e, –execute=COMMAND 执行`.wgetrc’格式的命令，wgetrc格式参见/etc/wgetrc或~/.wgetrc

### 记录和输入文件参数 ###
    -o, –output-file=FILE 把记录写到FILE文件中
    -a, –append-output=FILE 把记录追加到FILE文件中

    -d, –debug 打印调试输出
    -q, –quiet 安静模式(没有输出)
    -v, –verbose 冗长模式(这是缺省设置)
    -nv, –non-verbose 关掉冗长模式，但不是安静模式

    -i, –input-file=FILE 下载在FILE文件中出现的URLs

    -F, –force-html 把输入文件当作HTML格式文件对待
    -B, –base=URL 将URL作为在-F -i参数指定的文件中出现的相对链接的前缀
    –sslcertfile=FILE 可选客户端证书
    –sslcertkey=KEYFILE 可选客户端证书的KEYFILE
    –egd-file=FILE 指定EGD socket的文件名

### 下载参数 ###
    –bind-address=ADDRESS 指定本地使用地址(主机名或IP，当本地有多个IP或名字时使用)
    -O –output-document=FILE 把文档写到FILE文件中
    -t, –tries=NUMBER 设定最大尝试链接次数(0 表示无限制).
    -nc, –no-clobber 不要覆盖存在的文件或使用.#前缀
    -c, –continue 接着下载没下载完的文件
    –progress=TYPE 设定进程条标记
    -N, –timestamping 不要重新下载文件除非比本地文件新
    -S, –server-response 打印服务器的回应
    –spider 不下载任何东西
    -T, –timeout=SECONDS 设定响应超时的秒数
    -w, –wait=SECONDS 两次尝试之间间隔SECONDS秒
    –waitretry=SECONDS 在重新链接之间等待1…SECONDS秒
    –random-wait 在下载之间等待0…2*WAIT秒
    -Y, –proxy=on/off 打开或关闭代理
    -Q, –quota=NUMBER 设置下载的容量限制
    –limit-rate=RATE 限定下载输率

### 目录参数 ###
    -nd –no-directories 不创建目录
    -x, –force-directories 强制创建目录
    -nH, –no-host-directories 不创建主机目录
    -P, –directory-prefix=PREFIX 将文件保存到目录 PREFIX/…
    –cut-dirs=NUMBER 忽略 NUMBER层远程目录

### HTTP 选项参数 ###
    –http-user=USER 设定HTTP用户名为 USER.
    –http-passwd=PASS 设定http密码为 PASS
    -C, –cache=on/off 允许/不允许服务器端的数据缓存 (一般情况下允许)
    -E, –html-extension 将所有text/html文档以.html扩展名保存
    –ignore-length 忽略 `Content-Length’头域
    –header=STRING 在headers中插入字符串 STRING
    –proxy-user=USER 设定代理的用户名为 USER
    –proxy-passwd=PASS 设定代理的密码为 PASS
    –referer=URL 在HTTP请求中包含 `Referer: URL’头
    -s, –save-headers 保存HTTP头到文件
    -U, –user-agent=AGENT 设定代理的名称为 AGENT而不是 Wget/VERSION
    –no-http-keep-alive 关闭 HTTP活动链接 (永远链接)
    –cookies=off 不使用 cookies
    –load-cookies=FILE 在开始会话前从文件 FILE中加载cookie
    –save-cookies=FILE 在会话结束后将 cookies保存到 FILE文件中

### FTP 选项参数 ###
    -nr, –dont-remove-listing 不移走 `.listing’文件
    -g, –glob=on/off 打开或关闭文件名的 globbing机制
    –passive-ftp 使用被动传输模式 (缺省值).
    –active-ftp 使用主动传输模式
    –retr-symlinks 在递归的时候，将链接指向文件(而不是目录)

### 递归下载参数 ###
    -r, –recursive 递归下载－－慎用!
    -l, –level=NUMBER 最大递归深度 (inf 或 0 代表无穷)
    –delete-after 在现在完毕后局部删除文件
    -k, –convert-links 转换非相对链接为相对链接
    -K, –backup-converted 在转换文件X之前，将之备份为 X.orig
    -m, –mirror 等价于 -r -N -l inf -nr
    -p, –page-requisites 下载显示HTML文件的所有图片

### 递归下载中的包含和不包含(accept/reject) ###
    -A, –accept=LIST 分号分隔的被接受扩展名的列表
    -R, –reject=LIST 分号分隔的不被接受的扩展名的列表
    -D, –domains=LIST 分号分隔的被接受域的列表
    –exclude-domains=LIST 分号分隔的不被接受的域的列表
    –follow-ftp 跟踪HTML文档中的FTP链接
    –follow-tags=LIST 分号分隔的被跟踪的HTML标签的列表
    -G, –ignore-tags=LIST 分号分隔的被忽略的HTML标签的列表
    -H, –span-hosts 当递归时转到外部主机
    -L, –relative 仅仅跟踪相对链接
    -I, –include-directories=LIST 允许目录的列表
    -X, –exclude-directories=LIST 不被包含目录的列表
    -np, –no-parent 不要追溯到父目录
    wget -S –spider url 不下载只显示过程





## 例子和技巧 ##

### 使用wget下载单个文件 ###
    wget http://www.minjieren.com/wordpress-3.1-zh_CN.zip

###  使用wget -O 下载，并保存为其他文件名的文件 ###
    wget -O wordpress.zip http://www.minjieren.com/download.aspx?id=1080

说明：wget默认会以最后一个符合”/”的后面的字符来命令，对于动态链接的下载通常文件名会不正确。
错误：下面的例子会下载一个文件并以名称download.aspx?id=1080保存

    wget http://www.minjieren.com/download?id=1

即使下载的文件是zip格式，它仍然以download.php?id=1080命令。
正确：为了解决这个问题，我们可以使用参数-O来指定一个文件名：

    wget -O wordpress.zip http://www.minjieren.com/download.aspx?id=1080

### 使用 wget -limit-rate 限速下载 ###
    wget --limit-rate=300k http://www.minjieren.com/wordpress-3.1-zh_CN.zip

说明： wget默认使用全部带宽

### 使用 wget -c 断点续传 ###
