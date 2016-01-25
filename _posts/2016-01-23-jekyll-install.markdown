---
layout: post
title:  "windows下jekyll的安装以及github个人主页的搭建"
date:   2016-01-23 14:57:55
categories: jekyll update
---

* 一.jekyll 安装
	+ jeky是什么?
		- Jekyll（发音/'dʒiːk əl/，"杰克尔"）是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站。其实在github上搭建个人主页，jekyll是不需要的，使用jekyll一方面是需要根据模板生成静态网页，另一方面是在本地进行测试，测试成功之后再提交到github，否则要每次都往github上push的话就很麻烦了。 
		- github 本身是支持jekyll的， 所以在[http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html](这篇博客)中，博主是直接手动建好那些框架文件，然后直接提交到github上，github本身就会执行类似于 'jekyll build'的命令进行静态网页的生成.
	+ 安装ruby
		- 下载: [http://rubyinstaller.org/downloads/](下载地址), 如果你是新手，对ruby不熟悉，建议下载2.1.X版本,我下载的是2.1.7(x64)版本的(我的电脑是64位的)
		- 安装: 在安装过程中要注意的一点是选择安装位置的时候记得把 'Add Ruby executables to your PATH' 勾选,这样能在cmd中执行ruby 命令，否则需要手动在环境变量中添加ruby
		- 完成: 在cmd中输入 'ruby -v'测试是否安装成功
	 
* 二.个人主页的搭建
下面介绍我在使用jekyll 在github上搭建个人主页的过程(更新中)  

 

1. 在github上新建名为test的repo, 并将其pull到本地

2. 安装ruby

	+ abc
		* sdfsdfasdf
		* sdfsdfsdf
	+ sdfsdf
	+ sdfsdfsdf

3. 安装DevKit

4. 安装bundler

5. 安装jekyll

6. 生成myblog框架文件

7. 运行查看效果

8. push

---

  
参考:  

[http://lee.logdown.com/posts/165890/ruby-on-windows-7-to-install-ruby-on-rails](http://lee.logdown.com/posts/165890/ruby-on-windows-7-to-install-ruby-on-rails)  

[https://help.github.com/articles/using-jekyll-with-pages/](https://help.github.com/articles/using-jekyll-with-pages/)  

[http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
