## 错误码
MINI_VERSION_NAME_DUPLICATE（该名称已被使用，请输入新名称）。 

## 问题描述
代商家调用 alipay.open.mini.version.audit.apply（小程序提交审核）提交小程序审核时报错 "sub_code":"MINI_VERSION_NAME_DUPLICATE","sub_msg":"该名称已被使用，请输入新名称"。 

## 问题原因
在调用提交小程序审核接口时修改小程序应用名称 app_name，输入的名称已经被使用。 

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）

## 解决方案
输入新的应用名称 app_name，重新调用小程序提交审核接口。<br />**注意：**

- 一旦上架过提审就不能修改应用名称。
- 小程序应用名称修改，建议参考 [小程序运营规范](https://opendocs.alipay.com/b/03ajj7)，避免审核被驳回。

 
