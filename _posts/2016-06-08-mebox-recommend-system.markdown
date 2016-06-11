---
layout: post
title:  "米盒项目中的推荐系统的实现"
date:   2016-06-08 12:50:00
categories: java recommend-system
---
这篇博客记录的是在米盒项目的推荐需求中使用到的推荐算法  

1. 基于用户的协同过滤  
UserBasedCF的核心思想主要是找到和目标用户兴趣相似的用户集合，然后给目标用户推荐这个集合的用户喜欢的物品。关键在于计算用户与用户之间的兴趣相似度。这里主要使用余弦相似度来计算：  
![用户相似度计算公式](http://mmbiz.qpic.cn/mmbiz/sXiaukvjR0RBpprQopxicAvwhWZNmcr4icpLCX8vXkaiatphvtcicysaDicwb6TtlZk5oLicUYkRzT924VruJDqn7JmWA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)  

wuv 代表用户 u 与 v 之间的兴趣相似度，N(u)表示用户 u 曾经喜欢过的物品集合, N(v) 表示用户 v 曾经喜欢过的物品集合。  


2. 逐步实现  


参考资料:  
1. [推荐系统学习：协同过滤实现](http://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650342703&idx=1&sn=04aa3d0c196664da72e6f973394731fb&scene=0#wechat_redirect)  
2. [实时推荐系统的3种方式](http://www.jianshu.com/p/356656ce2901)