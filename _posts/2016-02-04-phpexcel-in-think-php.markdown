---
layout: post
title:  "Using phpexcel in think php!"
date:   2016-02-04 22:25:00
categories: php
---
1. 背景及准备  
	* 实现excel导入导出的功能
	* [PhpExcel](http://phpexcel.codeplex.com/) 是php操作excel的类库，类似的还有phpword,见我的一个[在线word编辑器项目](https://github.com/DengrongGuan12/wordeditor)
    * 下载PhpExcel,在ThinkPHP/Library/Vendor下新建目录Excel,将解压得到的`PhpExcel目录`及`PhpExcel.php文件`放置于刚刚新建的目录中 

2. 代码及解释  
	* 引入  
	{% highlight ruby %}
    vendor('Excel.PHPExcel.IOFactory');
	{% endhighlight %}  

	* 调用 导入解析(代码不完整)
{% highlight ruby %}
$file = $_FILES['scoresheet'];
$upload = new \Think\Upload();
$upload->exts      =     array('xls','xlsx');
$upload->rootPath  =   C("FILE_ROOT_PATH");
$upload->savePath  =   'course_'.$courseId.'/';
$upload->autoSub = false;
$upload->replace = true;

$upload->saveName = $name;
$info   =   $upload->uploadOne($file);
if(!$info) {//
    $this->ajaxReturn(['result'=>['status'=>0,'errorMsg'=>$upload->getError()]],'JSON');
}
$filePath =  C("FILE_ROOT_PATH").$info['savepath'].$info['savename'];
$inputFileType = \PHPExcel_IOFactory::identify($filePath); //自动识别excel版本
$reader = \PHPExcel_IOFactory::createReader($inputFileType);
$PHPExcel = $reader->load($filePath); // 载入excel文件
$sheet = $PHPExcel->getSheet(0); // 读取第一個工作表
$highestRow = $sheet->getHighestRow(); // 取得总行数
//$highestColumn = $sheet->getHighestColumn(); 取得总列数

/** 循环读取每个单元格的数据 */
$dataset = [];
for ($row = 2; $row <= $highestRow; $row++){//行数是以第2行开始
    $dataset[] = ['id'=>$sheet->getCell('A'.$row)->getValue(),'score'=>$sheet->getCell('D'.$row)->getValue(),'remark'=>$sheet->getCell('E'.$row)->getValue()];
}
{% endhighlight %}  

	* 调用 导出生成(代码不完整)  
{% highlight ruby %}
$phpExcel = new \PHPExcel();
$phpExcel->setActiveSheetIndex(0)->setCellValue('A1','ID');
$phpExcel->setActiveSheetIndex(0)->setCellValue('B1','学号');
$phpExcel->setActiveSheetIndex(0)->setCellValue('C1','姓名');
$phpExcel->setActiveSheetIndex(0)->setCellValue('D1','入学年份');
$phpExcel->setActiveSheetIndex(0)->setCellValue('E1','院系');
$i = 2;
foreach($students as $student){
    $phpExcel->setActiveSheetIndex(0)->setCellValue('A'.$i,$student['id']);
    $phpExcel->setActiveSheetIndex(0)->setCellValue('B'.$i,$student['schoolIdentify']);
    $phpExcel->setActiveSheetIndex(0)->setCellValue('C'.$i,$student['name']);
    $phpExcel->setActiveSheetIndex(0)->setCellValue('D'.$i,$student['grade']);
    $phpExcel->setActiveSheetIndex(0)->setCellValue('E'.$i,$student['department']);
    $i++;
}
$phpExcel->getActiveSheet()->setTitle('students');
$phpExcel->setActiveSheetIndex(0);
$excelWriter = \PHPExcel_IOFactory::createWriter($phpExcel,'Excel2007');
$saveName = C("FILE_ROOT_PATH").'course_'.$courseId.'/students_export.xlsx';
$excelWriter->save($saveName);
header("Content-type: application/octet-stream");
header('Content-Disposition: attachment; filename="'.'students_export.xlsx'.'"');
header("Content-Length: ". filesize($saveName));
readfile($saveName);
{% endhighlight %}  