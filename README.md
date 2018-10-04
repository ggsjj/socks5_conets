# socks5_conets
手工搭建 只可以conets 6   7


 下面我们将用SS5在Linux上搭建一个Socks5 Proxy Server，具体过程如下：
 
 首先，编译安装SS5需要先安装一些依赖组件

yum -y install gcc gcc-c++ automake make pam-devel openldap-devel cyrus-sasl-devel openssl-devel

 接下来，我们从 http://ss5.sourceforge.net/ 下载SS5最新版本的源代码后，开始编译安装：
 
 tar zxvf ./ss5-3.8.9-8.tar.gz

 cd ss5-3.8.9

 ./configure
 
 make
 
 make install 
 
让SS5随系统一起启动

chmod +x /etc/init.d/ss5

chkconfig --add ss5

chkconfig --level 345 ss5 on

开启用户名密码验证机制

vi /etc/opt/ss5/ss5.conf

在ss5.conf中找到auth和permit两行，按照下面的格式进行修改

auth 0.0.0.0/0 - u

permit u 0.0.0.0/0 - 0.0.0.0/0 - - - - -

设置用户名和密码

vi /etc/opt/ss5/ss5.passwd

一行一个账号，用户名和密码之间用空格间隔，例如：

user1 123

user2 234

设置端口vi /etc/sysconfig/ss5

在/etc/sysconfig/ss5这个文件中，添加下面这一行命令，-b后面的参数代表监听的ip地址和端口号

  #Add startup option hereS
  
  S5_OPTS=" -u root -b 0.0.0.0:8080"

启动service ss5 start

