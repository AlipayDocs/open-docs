## 错误码
AE0515022101 

## 错误描述
上传商品信息接口报："sub_code":"AE0515022101","sub_msg":"参数不合法property_value不能为空"。 

## 涉及接口
ant.merchant.expand.item.open.create（上传商品信息接口）

## 报错原因
property_value 参数入参字符为空导致。 

## 解决方案
property_list 为选填参数，如若入参，property_key 和 property_value 必填且必须在 32 个字符之内、不能为空""，修改 property_value 入参值在 32 个字符之内。<br /> 
