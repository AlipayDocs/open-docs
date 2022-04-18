## 简介
适用于符合 .Net Standard 2.0 规范的各类微软框架（如：.Net Framework >= 4.6.1、.Net Core >= 2.0 等）。<br />.Net Framework（3.5 ~ 4.6）的用户可以继续使用 [AlipaySDKNet](https://www.nuget.org/packages/AlipaySDKNet/)。

## 下载地址

- [NuGet 项目依赖](https://www.nuget.org/packages/AlipaySDKNet.Standard/)
- [GitHub 项目主页](https://github.com/alipay/alipay-sdk-net-all)

## 示例代码

### 普通调用示例
```csharp
IAopClient client = new DefaultAopClient("https://openapi.alipay.com/gateway.do", APPID, APP_PRIVATE_KEY, "json", "1.0", "RSA2", ALIPAY_PUBLIC_KEY, CHARSET, false);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称如：alipay.open.public.template.message.industry.modify 
AlipayOpenPublicTemplateMessageIndustryModifyRequest request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
request.BizContent="{" +
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," +
"    \"primary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" +
"  }";
AlipayOpenPublicTemplateMessageIndustryModifyResponse response = client.Execute(request); 
//调用成功，则处理业务逻辑
if(response.isSuccess()){
    //.....
}
```

### 普通调用示例（证书）
```csharp
//设置证书相关参数
CertParams certParams = new CertParams
{
    AlipayPublicCertPath = "支付宝公钥证书路径",
    AppCertPath = "商家应用证书路径",
    RootCertPath = "支付宝根证书路径"
};
IAopClient client = new DefaultAopClient("https://openapi.alipay.com/gateway.do", APPID, APP_PRIVATE_KEY, "json", "1.0", "RSA2", "utf-8", false, certParams);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称如：alipay.open.public.template.message.industry.modify 
AlipayOpenPublicTemplateMessageIndustryModifyRequest request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
request.BizContent="{" +
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," +
"    \"primary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" +
"  }";
AlipayOpenPublicTemplateMessageIndustryModifyResponse response = client.CertificateExecute(request); 
//调用成功，则处理业务逻辑
if(response.isSuccess()){
    //.....
}
```

### 图片上传接口调用示例
```csharp
IAopClient client = new DefaultAopClient("https://openapi.alipay.com/gateway.do", APPID, APP_PRIVATE_KEY, "json", "1.0", "RSA2", ALIPAY_PUBLIC_KEY, CHARSET, false);
// 实例化具体API对应的request类,类名称和接口名称对应，当前调用接口名称：alipay.offline.material.image.upload 
AlipayOfflineMaterialImageUploadRequest request = new AlipayOfflineMaterialImageUploadRequest();
request.setImageName("test");
//Windows请填写绝对路径，不支持相对路径；Linux支持相对路径
FileItem item = new FileItem("C:/Downloads/ooopic_963991_7eea1f5426105f9e6069/16365_1271139700.jpg");
request.setImageType("JPG");
request.ImageContent = item;
//执行API请求
AlipayOfflineMaterialImageUploadResponse response = alipayClient.Execute(request);
//调用成功，则处理业务逻辑
if(response.isSuccess()){
     //获取图片访问地址
    String imageUrl = response.getImageUrl();
    //.....
}
```

### 图片上传接口调用示例（证书）
```csharp
//设置证书相关参数
CertParams certParams = new CertParams
{
    AlipayPublicCertPath = "支付宝公钥证书路径",
    AppCertPath = "商家应用证书路径",
    RootCertPath = "支付宝根证书路径"
};
IAopClient client = new DefaultAopClient("https://openapi.alipay.com/gateway.do", APPID, APP_PRIVATE_KEY, "json", "1.0", "RSA2", "utf-8", false, certParams);
// 实例化具体API对应的request类,类名称和接口名称对应，当前调用接口名称：alipay.offline.material.image.upload 
AlipayOfflineMaterialImageUploadRequest request = new AlipayOfflineMaterialImageUploadRequest();
request.setImageName("test");
//Windows请填写绝对路径，不支持相对路径；Linux支持相对路径
FileItem item = new FileItem("C:/Downloads/ooopic_963991_7eea1f5426105f9e6069/16365_1271139700.jpg");
request.setImageType("JPG");
request.ImageContent = item;
//执行API请求
AlipayOfflineMaterialImageUploadResponse response = alipayClient.CertificateExecute(request);
//调用成功，则处理业务逻辑
if(response.isSuccess()){
     //获取图片访问地址
    String imageUrl = response.getImageUrl();
    //.....
}
```

### 用户授权接口调用示例
```csharp
IAopClient client = new DefaultAopClient("https://openapi.alipay.com/gateway.do", APPID, APP_PRIVATE_KEY, "json", "1.0", "RSA2", ALIPAY_PUBLIC_KEY, CHARSET, false);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.user.userinfo.share
AlipayUserUserinfoShareRequest request = new AlipayUserUserinfoShareRequest();
//授权类接口执行API调用时需要带上accessToken
AlipayUserUserinfoShareResponse response= client.Execute(request, "accessToken"); 
//业务处理
//...
```

### 用户授权接口调用示例（证书）
```csharp
//设置证书相关参数
CertParams certParams = new CertParams
{
    AlipayPublicCertPath = "支付宝公钥证书路径",
    AppCertPath = "商家应用证书路径",
    RootCertPath = "支付宝根证书路径"
};
IAopClient client = new DefaultAopClient("https://openapi.alipay.com/gateway.do", APPID, APP_PRIVATE_KEY, "json", "1.0", "RSA2", "utf-8", false, certParams);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.user.userinfo.share
AlipayUserUserinfoShareRequest request = new AlipayUserUserinfoShareRequest();
//授权类接口执行API调用时需要带上accessToken
AlipayUserUserinfoShareResponse response= client.CertificateExecute(request, "accessToken"); 
//业务处理
//...
```

### 应用授权接口调用示例（ISV 代理商家调用）
```csharp
IAopClient client = new DefaultAopClient("https://openapi.alipay.com/gateway.do", APPID, APP_PRIVATE_KEY, "json", "1.0", "RSA2", ALIPAY_PUBLIC_KEY, CHARSET, false);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify 
AlipayOpenPublicTemplateMessageIndustryModifyRequest request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
request.setBizContent("  {" +
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," +
"    \"primary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" +
"  }");
AlipayOpenPublicTemplateMessageIndustryModifyResponse response = client.Execute(request, null, "app_auth_token"); 
//调用成功，则处理业务逻辑
if(response.isSuccess()){
    //.....
}
```

### 应用授权接口调用示例（ISV 代理商家调用）（证书）
```csharp
//设置证书相关参数
CertParams certParams = new CertParams
{
    AlipayPublicCertPath = "支付宝公钥证书路径",
    AppCertPath = "商家应用证书路径",
    RootCertPath = "支付宝根证书路径"
};
IAopClient client = new DefaultAopClient("https://openapi.alipay.com/gateway.do", APPID, APP_PRIVATE_KEY, "json", "1.0", "RSA2", "utf-8", false, certParams);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify 
AlipayOpenPublicTemplateMessageIndustryModifyRequest request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
request.setBizContent("  {" +
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," +
"    \"primary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_code\":\"10001/20102\"," +
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" +
"  }");
AlipayOpenPublicTemplateMessageIndustryModifyResponse response = client.CertificateExecute(request, null, "app_auth_token"); 
//调用成功，则处理业务逻辑
if(response.isSuccess()){
    //.....
}
```


