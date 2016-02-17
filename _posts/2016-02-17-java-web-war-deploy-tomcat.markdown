---
layout: post
title:  "using maven to run and deploy war in tomcat of ubuntu"
date:   2016-02-17 15:02:00
categories: java web
---
这篇博客记录的是使用idea开发java web项目，并使用maven进行本地的测试及阿里云服务器的部署  
1. [项目地址](https://github.com/DengrongGuan12/tongbao)  

2. 导入运行  
  在使用maven导入依赖后就可以使用tomcat插件运行，如图是运行的配置,使用tomcat:run-war的方式是为了生成war文件方便部署到真实的服务器上  
  ![运行配置](http://i11.tietuku.com/0e5323e618b0314dt.jpg)  

3. 部署  
  参考[ubuntu tomcat部署项目](http://tianyongwei.logdown.com/posts/245849-linux-deployment-projects)  

4. 问题  
  这里我使用tomcat manage 中自带的部署方式，即在网页上上传war文件，但是上传之后发现无法start，什么错误也没报，这时想到查看日志文件，我采用的实时查看的方式:  
  在tomcat目录下的log文件中输入命令 `tail -f catalina.out` 即可.  
  重新部署，报错如下:  
  ![报错](http://i12.tietuku.com/8b81644f02dfc6bbt.jpg)  
  百度之后发现了问题所在,将model中的@Table删除即可，即只使用@Entity(name="user_t"),可能是hibernate的一个bug?  
  但是修正之后就发现了新的问题:  
  ![新的问题](http://i13.tietuku.com/63243c8fde24041ct.jpg)  
  有待解决!  