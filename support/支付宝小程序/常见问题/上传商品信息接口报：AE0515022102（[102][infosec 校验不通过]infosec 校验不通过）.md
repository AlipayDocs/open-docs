## 错误码
AE0515022102 

## 错误描述
上传商品信息接口报："sub_code":"AE0515022102","sub_msg":"[102][infosec 校验不通过]infosec 校验不通过"。 

## 涉及接口
ant.merchant.expand.item.open.create（上传商品信息接口）

## 报错原因
name 参数入参字符存在非法内容，命中敏感词汇导致。 

## 解决方案
name 参数修改传入的内容符合规范，剔除敏感词汇。<br /> 
