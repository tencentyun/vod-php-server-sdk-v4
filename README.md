# vod-php-server-sdk-v4
腾讯云点播4.0 ServerSDK(For PHP)

## 功能说明
vod-php-server-sdk是为了让PHP开发者能够在自己的代码里更快捷方便地使用点播上传功能而开发的SDK工具包，支持开发者指定并发上传分片数目及每个分片可重传的次数，用法参见示例代码demo.php。

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
