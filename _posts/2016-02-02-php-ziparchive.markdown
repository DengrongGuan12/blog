---
layout: post
title:  "Using php ZipArchive in think php!"
date:   2016-02-02 21:02:00
categories: php
---
1. 背景  
	* 实现批量下载的功能
	* ZipArchive 是php的扩展类，自php5.2版本以后就已经支持这个扩展,不需要手动修改php.ini

2. 代码及解释  
	* 添加公共函数  
	在'ThinkPHP/Common/functions.php' 添加函数'addFileToZip'  
	{% highlight ruby %}
	#=> 打包文件夹
function addFileToZip($path,$zip){
    $handler=opendir($path); #=> 打开当前文件夹由$path指定。
    while(($filename=readdir($handler))!==false){
        if($filename != "." && $filename != ".."){#=> 文件夹文件名字为'.'和‘..’，不要对他们进行操作
            $file = $path."/".$filename;
            if(is_dir($file)){#=> 如果读取的某个对象是文件夹，则递归
                addFileToZip($file, $zip);
            }else{ #=> 将文件加入zip对象
                $file_info_arr= pathinfo($file);
                $zip->addFile($file,$file_info_arr['basename']); #=> 这里采用这种方式是为了防止把路径也打包进去
            }
        }
    }
    closedir($path);
}
	{% endhighlight %}  

	* 调用 
{% highlight ruby %}
$path = C("FILE_ROOT_PATH").'course_'.$courseId.'/homework/'.$homeworkId;
$tmpPath = C("FILE_ROOT_PATH").'course_'.$courseId.'/homework/'.$homeworkId.'.zip';
if(file_exists($tmpPath)){
	unlink($tmpPath);
}
$zip=new \ZipArchive(); #=> 注意这里和下面的ZipArchive 前都使用'\',否则会报错
if($zip->open($tmpPath, \ZipArchive::CREATE)=== TRUE){
	addFileToZip($path, $zip); #=> 调用方法，对要打包的根目录进行操作，并将ZipArchive的对象传递给方法
	$zip->close(); #=> 关闭处理的zip文件
}
{% endhighlight %}  

	* 下载  
{% highlight ruby %}
header("Content-type: application/octet-stream");
header('Content-Disposition: attachment; filename="' . $homeworkId.'.zip' . '"');
header("Content-Length: ". filesize($tmpPath));
readfile($tmpPath);
{% endhighlight %}  

    * 中文问题  
    在测试过程中发现文件名中有中文的会自动跳过（通过数据库表中存的path向zip中添加文件，数据库path字段是utf-8编码）,在百度之后发现采用  
    `iconv("utf-8","gb2312",$path)`  
    方式可以解决这个问题，但是这种方案只针对不以中文开头的文件，但是如果文件是以中文开头，中文会被省略，有待解决.
