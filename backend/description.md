# 常见概念
## Java EE与Java SE区别
#### javaSE 是 jdk jvm 以及自带的api合集的具体实现。
#### javaEE 是基于javase而发展出来的一套规范接口。主要规范了Web和软件开发
如果直接使用java SE搭建服务器也行，可以使用标准CGI。但是在java EE中有着更好、更规范的开发(JSP,servlet,jdbc等)。另外J2EE和JavaEE没有区别，只不过J2EE是以前使用的名字。
## 注解

> http://blog.csdn.net/briblue/article/details/73824058
## xml、properties与yaml
在程序开发中，我们经常会有一些配置程序用于。比如我们要指明本项目的数据库名称，定时器配置等。如果写在代码里，那么对于编译型语言的java我们如果更改了配置就需要重新部署了。对于非常庞多复杂的程序代码，如果不小心改错了地方，还可能导致原先的代码会无法缺失了。这时候我们就需要配置化了。

在Spring开发中有三种配置粉文件。这三种文件可以做到基本的代码无关化。如果要让代码更加的解耦，则应该尽量合理的使用配置文，但是过多的配置文件会让我们的系统变得更加的动态化，需要多次加载，导致内存占用大，系统变慢等。
主要格式有xml、properties与yml
- xml类似于html比较严格，而且有很明显的树形结构
- properties
## json与x-www-form-urlencoded
在网络传输中
## Restful                                                            
## BS模式
## MVC模式
## 框架