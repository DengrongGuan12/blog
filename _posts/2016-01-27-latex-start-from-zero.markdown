---
layout: post
title:  "Latex-Start from zero!"
date:   2016-01-27 15:50:55
categories: latex
---
1. 简介

2. 安装(windows 64位)

	+ windows 64位 发行版 MikeTex 安装
		* [下载地址](http://pan.baidu.com/s/1bnMWnbp)
	+ windows 64位 编辑器 WinEdt 安装
		* [下载地址](http://pan.baidu.com/s/1mh2B1oO)

3. 使用
	
	* hello world
		+ 新建文件夹 'helloworld'
		+ 新建文件 'helloworld.tex'
		+ 使用Texworks 打开, 输入内容:
		
		{% highlight ruby %}
		%helloworld.tex
		\documentclass{article}
		\begin{document}
			Hello, World!
		\end{document}
		print_hi('Tom')
		{% endhighlight %}