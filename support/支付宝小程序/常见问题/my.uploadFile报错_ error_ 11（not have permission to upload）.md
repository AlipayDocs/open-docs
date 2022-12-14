## 错误码
11

## 报错描述
my.uploadFile报错: error: 11（not have permission to upload）。 

## 涉及接口
[my.uploadFile](https://opendocs.alipay.com/mini/api/kmq4hc)。

## 报错原因
使用了 my.saveFile 保存文件后返回的 apFilePath 进行上传。 

## 解决方案
出于安全策略，不能使用 my.saveFile 保存文件后返回的 apFilePath 作为上传 filePath 的入参。<br /> 
