# 主要功能介绍

## 目录
![屏幕快照 2018-01-23 下午1.58.25.png](https://i.loli.net/2018/01/23/5a66cf1258dcf.png)
着重讲下两个地方，其他的大家点开看看大概都可以明白。
### 安全组:这里可以设置公网IP要暴露的端口

大部分同学都是没有设置好要暴漏的socket导致无法正常访问

这里又要提高一个概念:网络套接字(socket)。访问任何一个网站不仅需要对应的IP，还要对应的端口。学过计算机网络的都会知道我们要进行网络通信就要通过socket,socket由协议,地址，端口组成。每一个软件服务或者说进程进行网络通信都要用对应的socket。两个socket进行连接就可以建立一个TCP连接进行网络通信了。

这里再说说我们常用端口,当然这些服务用这些端口只是我们约定的。如果要改成其他端口也不是不可以

|端口服务|端口号|描述|
|-|-|
|SSH服务|22|用于远程管理linux|
|MySQL服务|3306||
|http|80|
|https|443|
|Tomcat服务|8080|

大家设置好了暴漏的端口后，就可以先通过telnet来测试访问了
    telnet 118.89.52.145 8080

成功后会显示尝试连接
![屏幕快照 2018-01-23 下午5.31.43.png](https://i.loli.net/2018/01/23/5a6701784c1f5.png)

失败则会显示拒绝
![屏幕快照 2018-01-23 下午5.31.58.png](https://i.loli.net/2018/01/23/5a6703b150559.png)

### 云主机

安装系统这里由官方提供好的原生系统镜像(公共镜像)和一些别人已经转好开发环境的镜像(服务市场)

![屏幕快照 2018-01-23 下午6.58.40.png](https://i.loli.net/2018/01/23/5a67157eae0ba.png)

这里我还是推荐先从原生开始，顺便练习命令行操作

这里我以CentOS 7作为案例进行安装