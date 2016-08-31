# Linux(CentOS)下JDK安装 #

1. 下载jdk压缩包
2. 使用rz命令，将压缩包上传到Linux
3. 在CentOS系统中，一般习惯将jdk安装在 /usr/local 路径下
  > cd /usr/local

  > mkdir java

  > rz

  > tar -zxvf jdk-7u79-linux-x64.tar.gz

4. 解压后，配置环境变量

  > vi /etc/profile

  在文件末尾添加

        JAVA_HOME=/usr/program/jdk1.7.0_79
        JRE_HOME=$JAVA_HOME/jre
        PATH=$PATH:$JAVA_HOME/bin
        CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
        export JAVA_HOME
        export JRE_HOME
        export PATH
        export CLASSPATH

5. 刷新配置文件，使配置文件生效
  > source /etc/profile


# Linux(CentOS)下Tomcat使用 #
