## 错误码
CATEGORY_NUM_IS_INVALID（类目数量需要是1-4个）。 

## 错误描述
alipay.open.mini.version.audit.apply（小程序提交审核接口）报 CATEGORY_NUM_IS_INVALID（类目数量需要是1-4个）。 

## 涉及接口

- [alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）
- [alipay.open.mini.baseinfo.modify](https://opendocs.alipay.com/mini/03l8c5)（小程序修改基础信息）

## 解决方案
当小程序没有设置类目时 app_category_ids 不能为空，可通过 [alipay.open.mini.category.query](https://opendocs.alipay.com/mini/03l8c6)（小程序类目树查询接口）进行查询，一级类目和二级类目使用 _ 进行连接，如：107209_107306。<br /> <br /> 
