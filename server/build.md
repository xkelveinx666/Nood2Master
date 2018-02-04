# 服务器环境搭建
这里我以CentOS 7作为案例进行安装

首先通过ssh进行连接

    //ssh <username>@ip
    ssh root@118.89.52.145
    //成功连接后查看下Linux内核版本
    cat /proc/version 
    //先更新下已有软件包
    yum update

### 这里安装的是java环境,包含nginx，jre，tomcat，mysql

来到命令行安装方式自然和带Gui(图形界面)的windows不一样了，当然对于我们编程常用的文件却更加方便了

## nginx
nginx差不多可以算是一个代理中介。即使他也是一个服务器，但是动态处理网页(JSP)并不是他的强项，但是对于静态资源和连接控制确实非常强悍。目前，基本都会使用nginx进行端口反向代理、负载均衡。同时nginx还可以代理socket，可以将8080的tomcat代理到80端口上。

#### 反向代理:由服务端动态分配并决定处理本次请求的服务器
#### 负载均衡:根据使用资源情况合理的将请求分配给多台服务器中

    //搜索nginx包是否存在
    yum search nginx
    //如果有nginx.x86_64则说明已有nginx包了，不然请输入以下命令添加源 
    yum install epel-release
    //安装nginx
    yum install nginx

然后就可以直接输入外网的IP地址，应该就可以看到部署好的nginx，接下来就是配置了。

![屏幕快照 2018-01-25 下午3.00.58.png](https://i.loli.net/2018/01/25/5a698137d4d71.png)

具体配置nginx可以看看别人的文章

https://www.extlight.com/2017/10/18/Nginx-%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/
## java
在Linux中由于某些原因存在着两种java,一种是oracle官方的sun-jdk，另一种是Google的open-jdk。区别也不是很大，目前主流都是使用open-jdk(比较好装)。

    //yum安装java(-y 添加了参数，用于安装时自动输入y确认)
    yum install java -y
    //查看是否安装
    java -version
## tomcat
tomcat在yum中没有官方的源，所以我们使用安装包的方式进行安装。这个在linux下也是常用的方式。这里必须先学习下wget命令

### wget
wget是Linux中一种下载工具。用于命令行的软件下载，使用wget下载将会进行不断重试，能提供一个非常稳定的下载。支持断点续传，和HTTP、FTP下载。更多好处大家可以自己再多学习学习
> http://man.linuxde.net/wget
### tar
tar是Linux中的打包工具。有点类似于winrar的功能。可以将多个文件打包或解压。
> http://man.linuxde.net/tar

    //切换到系统临时文件夹
    cd /tmp
    //下载包我们需要用到wget命令 
    //http://mirror.bit.edu.cn/apache/tomcat/tomcat-9/v9.0.4/bin/apache-tomcat-9.0.4.tar.gz
    wget http://mirror.bit.edu.cn/apache/tomcat/tomcat-9/v9.0.4/bin/apache-tomcat-9.0.4.tar.gz
    //创建要放置tomcat的文件夹
    mkdir /usr/bin/tomcat
    //解压tomcat到指定文件夹
    tar xvf apache-tomcat-9.0.4.tar.gz -C /usr/bin/tomcat --strip-components=1
    //切换到tomcat目录下并且赋予权限
    cd /usr/bin/tomcat && chmod -R g+r conf webapps work temp logs
    //测试开启tomcat,显示Tomcat Started基本没问题了。然后再通过ip:8080看看tomcat
    cd bin && sh starup.sh
更多配置
> https://www.howtoforge.com/tutorial/how-to-install-tomcat-on-centos/
> http://blog.csdn.net/smile_miracle/article/details/53185790
## mysql
mysql作为我们的数据库。我们在Linux下更没有必要使用gui(图形界面)了。而且mysql在yum下没有直接安装方式(yum install mysql 将会安装Maria DB)，这里我们将使用rpm二进制方式安装(源码安装可能会遇到内存不够的问题)。
    //rpm包是linux下的一种软件包，能自动解决软件以来问题。就像window下的.exe方式安装。但是以来关系比较复杂
   wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
   rpm -ivh mysql57-community-release-el7-11.noarch.rpm
    //启动mysql并查看临时密码
   systemctl start mysqld && grep 'temporary password' /var/log/mysqld.log
   ![屏幕快照 2018-01-26 下午6.11.16.png](https://i.loli.net/2018/01/26/5a6b221a3802b.png)
   //输入上面的密码
   mysql -u root -p
   //设置密码等级
   set global validate_password_policy=0;
   //退出mysql
   exit;
   //配置mysql
   mysql_secure_installation

![屏幕快照 2018-01-27 下午4.08.01.png](https://i.loli.net/2018/01/27/5a6c337c71fd2.png)
最后在mysql workbench设置下带SSH的远程控制。上面的是SSH密码，下面的是mysql的密码