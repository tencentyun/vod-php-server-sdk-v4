# vod-php-server-sdk-v4
腾讯云点播4.0 ServerSDK(For PHP)

## 功能说明
vod-php-server-sdk是为了让PHP开发者能够在自己的代码里更快捷方便地使用点播上传功能而开发的SDK工具包，支持开发者指定并发上传分片数目及每个分片可重传的次数、支持断点续传，用法参见"示例代码"demo.php。

## 示例代码
demo.php
```
<?php
error_reporting(E_ALL ^ E_NOTICE);
require_once './VodUpload.php';

$vod = new VodApi($config);
$vod->SetSecretId("AKIDvzvn***");
$vod->SetSecretKey("EHLKDE4***");
$vod->SetRegion("gz");
$vod->SetConcurrentNum(10); //设置并发上传的分片数目，不调用此函数时默认并发上传数为6
$vod->SetRetryTimes(10);    //设置每个分片可重传的次数，不调用此函数时默认值为5

/* $package: 上传的文件配置参数 */
$package = array(
    'fileName' => $argv[1],             //文件的绝对路径，包含文件名
    'dataSize' => 1024*1024,            //分片大小，单位Bytes
    'isTranscode' => 0,                 //是否转码
    'isScreenshot' => 0,                //是否截图
    'isWatermark' => 0,                 //是否添加水印
	'classId' => 0						//分类
);

$vod->AddFileTag("测试1");
$vod->AddFileTag("测试2");
$ret = $vod->UploadVideo($package);
if($ret !== 0)
{
    echo "upload error\n";
}
```

## 使用说明
1.在第一次使用云API之前，用户首先需要在[腾讯云网站](https://www.qcloud.com/document/product/266/1969#1.-.E7.94.B3.E8.AF.B7.E5.AE.89.E5.85.A8.E5.87.AD.E8.AF.81)申请安全凭证，安全凭证包括 SecretId 和 SecretKey, SecretId 是用于标识 API 调用者的身份，SecretKey是用于加密签名字符串和服务器端验证签名字符串的密钥。SecretKey 必须严格保管，避免泄露。申请之后，可到 https://console.qcloud.com/capi 查看已申请的密钥（SecretId及SecretKey）。

2.运行示例代码  
Linux命令行  
\#php demo.php 视频文件路径，如php demo.php test.mp4  
如果上传文件成功，终端输出如下log  
```
===InitUpload begin===
[InitUpload] recv:{"canRetry":0,"code":0,"codeDesc":" 0\n","message":"","sessionInfo":"{\"sessionKey\":\"xxx\"}"}

===UploadPart begin===

===FinishUpload begin===
[FinishUpload] recv:{"canRetry":0,"code":0,"codeDesc":"","fileId":"xxx","message":"","sessionInfo":"","url":"http:\/\/xxx.vod2.myqcloud.com\/vodxxx\/xxx\/f0.mp4"}
```
如果上传中断，可通过再次执行demo.php代码（php demo.php test.mp4）恢复上传（断点续传）。
