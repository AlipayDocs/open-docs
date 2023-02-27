# 错误码
INVALID_CATEGORY（输入的小程序类目不存在）。 

# 问题描述
接口报错 "subCode":"INVALID_CATEGORY","subMsg":"输入的小程序类目不存在","success":false。 

# 涉及接口
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核）

# 解决方案

- 检查 app_category_ids 入参类目是否正确，请输入合法的小程序类目，详细类目可以通过 [alipay.open.mini.category.query](https://opendocs.alipay.com/mini/03l8c6)（小程序类目树查询）接口查询。
- 检查类目使用范围，个人小程序只能使用对个人开放的类目，具体可参考 [小程序个人经营类目](https://opendocs.alipay.com/b/03al2n)。
- 入参类目格式是否正确，格式为：第一个一级类目_第一个二级类目；第二个一级类目_第二个二级类目（**如有三级类目需要加上三级类目**），如：107211_107242。
- 目前有两种类目：category_list（旧）和 mini_category_list（新）（新类目以 XS 开头，如 XS1007_XS2059_XS3062），如果使用的是新类目需使用 mini_category_ids 入参。如 SDK 接口没有该参数请升级 SDK 到最新。<br />**注意：**使用 mini_category_ids（**推荐**）后不再读取 app_category_ids 值，旧版前台类目将废弃。
```html
<!-- https://mvnrepository.com/artifact/com.alipay.sdk/alipay-sdk-java -->
<dependency>   
  <groupId>com.alipay.sdk</groupId> 
  <artifactId>alipay-sdk-java</artifactId>    
  <version>4.10.29.ALL</version>
</dependency>
```
 
