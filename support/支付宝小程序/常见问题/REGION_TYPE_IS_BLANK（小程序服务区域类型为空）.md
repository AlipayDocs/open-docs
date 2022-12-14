## 错误码
REGION_TYPE_IS_BLANK（小程序服务区域类型为空）。 

## 错误描述
alipay.open.mini.version.audit.apply（小程序提交审核接口）报 REGION_TYPE_IS_BLANK（小程序服务区域类型为空）。 

## 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）

## 解决方案

- region_type 为必选参数， 没有传入 region_type 参数。
- 如果 region_type=LOCATION 则需要传入 service_region_info。

 
