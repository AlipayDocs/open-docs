## 简介

适用于 Java 语言、JDK 版本 1.6 及以上的开发环境。

## 下载地址

- [Maven 项目依赖](https://search.maven.org/artifact/com.alipay.sdk/alipay-sdk-java)
- [GitHub 项目主页](https://github.com/alipay/alipay-sdk-java-all)

## 示例代码

### 普通调用示例

```java
//实例化客户端
AlipayClient alipayClient = new DefaultAlipayClient("https://openapi.alipay.com/gateway.do", APP_ID, APP_PRIVATE_KEY, "json", CHARSET, ALIPAY_PUBLIC_KEY, "RSA2");
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify
AlipayOpenPublicTemplateMessageIndustryModifyRequest request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
request.setBizContent("  {" +
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," +
"    \"primary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" +
" }");
AlipayOpenPublicTemplateMessageIndustryModifyResponse response = alipayClient.execute(request);
//调用成功，则处理业务逻辑
if(response.isSuccess()){
    //.....
}
```

### 普通调用示例（证书）

```java
//构造client
CertAlipayRequest certAlipayRequest = new CertAlipayRequest();
//设置网关地址
certAlipayRequest.setServerUrl("https://openapi.alipay.com/gateway.do");
//设置应用Id
certAlipayRequest.setAppId(app_id);
//设置应用私钥
certAlipayRequest.setPrivateKey(privateKey);
//设置请求格式，固定值json
certAlipayRequest.setFormat("json");
//设置字符集
certAlipayRequest.setCharset(charset);
//设置签名类型
certAlipayRequest.setSignType(sign_type);
//设置应用公钥证书路径
certAlipayRequest.setCertPath(app_cert_path);
//设置支付宝公钥证书路径
certAlipayRequest.setAlipayPublicCertPath(alipay_cert_path);
//设置支付宝根证书路径
certAlipayRequest.setRootCertPath(alipay_root_cert_path);
//构造client
AlipayClient alipayClient = new DefaultAlipayClient(certAlipayRequest);
//构造API请求
AlipayTradeQueryRequest request = new AlipayTradeQueryRequest();
//发送请求
AlipayTradeQueryResponse response = alipayClient.certificateExecute(request);
```

### 图片上传接口调用示例

```java
AlipayClient alipayClient = new DefaultAlipayClient("https://openapi.alipay.com/gateway.do", APP_ID, APP_PRIVATE_KEY, "json", CHARSET, ALIPAY_PUBLIC_KEY, "RSA2");
// 实例化具体API对应的request类,类名称和接口名称对应，当前调用接口名称：alipay.offline.material.image.upload
AlipayOfflineMaterialImageUploadRequest request = new AlipayOfflineMaterialImageUploadRequest();
request.setImageName("test");
//Windows请填写绝对路径，不支持相对路径；Linux支持相对路径
FileItem item = new FileItem("C:/Downloads/ooopic_963991_7eea1f5426105f9e6069/16365_1271139700.jpg");
request.setImageType("JPG");
request.setImageContent(item);
//执行API请求
AlipayOfflineMaterialImageUploadResponse response = alipayClient.execute(request);
//调用成功，则处理业务逻辑
if(response.isSuccess()){
     //获取图片访问地址
    String imageUrl = response.getImageUrl();
    //.....
}
```

### 图片上传接口调用示例（证书）

```java
//构造client
CertAlipayRequest certAlipayRequest = new CertAlipayRequest();
DefaultAlipayClient alipayClient = new DefaultAlipayClient(certAlipayRequest);
// 实例化具体API对应的request类,类名称和接口名称对应，当前调用接口名称：alipay.offline.material.image.upload
AlipayOfflineMaterialImageUploadRequest request = new AlipayOfflineMaterialImageUploadRequest();
request.setImageName("test");
//Windows请填写绝对路径，不支持相对路径；Linux支持相对路径
FileItem item = new FileItem("C:/Downloads/ooopic_963991_7eea1f5426105f9e6069/16365_1271139700.jpg");
request.setImageType("JPG");
request.setImageContent(item);
//执行API请求
AlipayOfflineMaterialImageUploadResponse response = alipayClient.certificateExecute(request);
//调用成功，则处理业务逻辑
if(response.isSuccess()){
     //获取图片访问地址
    String imageUrl = response.getImageUrl();
    //.....
}
```

### 用户授权接口调用示例

```java
AlipayClient alipayClient = new DefaultAlipayClient("https://openapi.alipay.com/gateway.do", APP_ID, APP_PRIVATE_KEY, "json", CHARSET, ALIPAY_PUBLIC_KEY, "RSA2");
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.user.userinfo.share
AlipayUserUserinfoShareRequest request = new AlipayUserUserinfoShareRequest();
//授权类接口执行API调用时需要带上accessToken
AlipayUserUserinfoShareResponse response= alipayClient.execute(request,"accessToken");
//业务处理
//...
```

### 用户授权接口调用示例（证书）

```java
//构造client
CertAlipayRequest certAlipayRequest = new CertAlipayRequest();
DefaultAlipayClient alipayClient = new DefaultAlipayClient(certAlipayRequest);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.user.userinfo.share
AlipayUserUserinfoShareRequest request = new AlipayUserUserinfoShareRequest();
//授权类接口执行API调用时需要带上accessToken
AlipayUserUserinfoShareResponse response = alipayClient.certificateExecute(request, "access_token");
```

### 应用授权接口调用示例（ISV 代理商家调用）

```java
AlipayClient alipayClient = new DefaultAlipayClient("https://openapi.alipay.com/gateway.do", APP_ID, APP_PRIVATE_KEY, "json", CHARSET, ALIPAY_PUBLIC_KEY, "RSA2");
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify
AlipayOpenPublicTemplateMessageIndustryModifyRequest request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
request.setBizContent("  { " +
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," +
"    \"primary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" +
"  }");
//ISV代理商家调用需要传入app_auth_token
request.putOtherTextParam("app_auth_token", "201511BBaaa6464f271f49e482f2e9fe63ca5F05");
AlipayOpenPublicTemplateMessageIndustryModifyResponse response = alipayClient.execute(request);
//调用成功，则处理业务逻辑
if(response.isSuccess()){
    //.....
}
```

### 应用授权接口调用示例（ISV 代理商家调用）（证书）

```java
//构造client
CertAlipayRequest certAlipayRequest = new CertAlipayRequest();
AlipayClient alipayClient = new DefaultAlipayClient(certAlipayRequest);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify
AlipayOpenPublicTemplateMessageIndustryModifyRequest request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
request.setBizContent("  { " +
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," +
"    \"primary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" +
"  }");
//ISV代理商家调用需要传入app_auth_token
request.putOtherTextParam("app_auth_token", "201511BBaaa6464f271f49e482f2e9fe63ca5F05");
//发送应用授权请求
AlipayTradeQueryResponse response = alipayClient.certificateExecute(request);
```
