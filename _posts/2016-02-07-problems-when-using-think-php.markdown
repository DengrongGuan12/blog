---
layout: post
title:  "Problems when using think php!"
date:   2016-02-04 22:25:00
categories: php
---
该篇博客持续记录在使用thinkphp时遇到的迷之问题  
1. getField()  
	问题代码(中文不支持,返回值迷之格式):  
{% highlight ruby %}
$model->join('student on user.id = student.user_id')
->join('department on student.department_id = department.id')
->where($condition)
->getField('user.id as id,user.name as name, department.name as department, user.school_identify as schoolIdentify',$num);
{% endhighlight %} 
    修正代码:  
 {% highlight ruby %}
$model->join('student on user.id = student.user_id')
->join('department on student.department_id = department.id')
->where($condition)->limit($num)
->getField('user.id as id,user.name as name, department.name as department, user.school_identify as schoolIdentify');
{% endhighlight %}    