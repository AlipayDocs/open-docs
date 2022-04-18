## 简介
适用于 PHP 5.5 以上的开发环境。

## 下载地址
[GitHub 项目主页](https://github.com/alipay/alipay-sdk-php-all)

## 示例代码

### 普通调用示例
```php
$c = new AopClient;
$c->gatewayUrl = "https://openapi.alipay.com/gateway.do";
$c->appId = "app_id";
$c->rsaPrivateKey = '请填写开发者私钥去头去尾去回车，一行字符串' ;
$c->format = "json";
$c->charset= "GBK";
$c->signType= "RSA2";
$c->alipayrsaPublicKey = '请填写支付宝公钥，一行字符串';
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify
$request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
$request->setBizContent = "{" .
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," .
"    \"primary_industry_code\":\"10001/20102\"," .
"    \"secondary_industry_code\":\"10001/20102\"," .
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" .
" }";
$response= $c->execute($request);
```

### 普通调用示例（证书）
```php
$c = new AopCertClient;
$appCertPath = "应用证书路径（要确保证书文件可读），例如：/home/admin/cert/appCertPublicKey.crt";
$alipayCertPath = "支付宝公钥证书路径（要确保证书文件可读），例如：/home/admin/cert/alipayCertPublicKey_RSA2.crt";
$rootCertPath = "支付宝根证书路径（要确保证书文件可读），例如：/home/admin/cert/alipayRootCert.crt";
$c->gatewayUrl = "https://openapi.alipay.com/gateway.do";
$c->appId = "app_id";
$c->rsaPrivateKey = '请填写开发者私钥去头去尾去回车，一行字符串' ;
$c->format = "json";
$c->charset= "GBK";
$c->signType= "RSA2";
//调用getPublicKey从支付宝公钥证书中提取公钥
$c->alipayrsaPublicKey = $c->getPublicKey($alipayCertPath);
//是否校验自动下载的支付宝公钥证书，如果开启校验要保证支付宝根证书在有效期内
$c->isCheckAlipayPublicCert = true;
//调用getCertSN获取证书序列号
$c->appCertSN = $c->getCertSN($appCertPath);
//调用getRootCertSN获取支付宝根证书序列号
$c->alipayRootCertSN = $c->getRootCertSN($rootCertPath);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify
$request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
$request->setBizContent = "{" .
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," .
"    \"primary_industry_code\":\"10001/20102\"," .
"    \"secondary_industry_code\":\"10001/20102\"," .
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" .
" }";
$response= $c->execute($request);
```

### 图片上传接口调用示例
```php
$c = new AopClient;
$c->gatewayUrl = "https://openapi.alipay.com/gateway.do";
$c->appId = "app_id";
$c->rsaPrivateKey = '请填写开发者私钥去头去尾去回车，一行字符串' ;
$c->format = "json";
$c->charset = "GBK";
$c->signType= "RSA2";
$c->alipayrsaPublicKey = '请填写支付宝公钥，一行字符串';
//实例化具体API对应的request类,类名称和接口名称对应，当前调用接口名称：alipay.offline.material.image.upload 
$request = new AlipayOfflineMaterialImageUploadRequest();
$request->setImageName("测试文件");
$request->setImageType("jpg");
//Windows请填写绝对路径，不支持相对路径；Linux支持相对路径
$request->setImageContent("@"."本地文件路径"); 
$response = $c->execute($request);
//获取图片地址
$response->getImageUrl();
```

### 图片上传接口调用示例（证书）
```php
$c = new AopCertClient;
$appCertPath = "应用证书路径（要确保证书文件可读），例如：/home/admin/cert/appCertPublicKey.crt";
$alipayCertPath = "支付宝公钥证书路径（要确保证书文件可读），例如：/home/admin/cert/alipayCertPublicKey_RSA2.crt";
$rootCertPath = "支付宝根证书路径（要确保证书文件可读），例如：/home/admin/cert/alipayRootCert.crt";
$c->gatewayUrl = "https://openapi.alipay.com/gateway.do";
$c->appId = "app_id";
$c->rsaPrivateKey = '请填写开发者私钥去头去尾去回车，一行字符串' ;
$c->format = "json";
$c->charset = "GBK";
$c->signType= "RSA2";
//调用getPublicKey从支付宝公钥证书中提取公钥
$c->alipayrsaPublicKey = $c->getPublicKey($alipayCertPath);
//是否校验自动下载的支付宝公钥证书，如果开启校验要保证支付宝根证书在有效期内
$c->isCheckAlipayPublicCert = true;
//调用getCertSN获取证书序列号
$c->appCertSN = $c->getCertSN($appCertPath);
//调用getRootCertSN获取支付宝根证书序列号
$c->alipayRootCertSN = $c->getRootCertSN($rootCertPath);
//实例化具体API对应的request类,类名称和接口名称对应，当前调用接口名称：alipay.offline.material.image.upload 
$request = new AlipayOfflineMaterialImageUploadRequest();
$request->setImageName("测试文件");
$request->setImageType("jpg");
//Windows请填写绝对路径，不支持相对路径；Linux支持相对路径
$request->setImageContent("@"."本地文件路径"); 
$response = $c->execute($request);
//获取图片地址
$response->getImageUrl();
```

### 用户授权接口调用示例
```php
$c = new AopClient;
$c->gatewayUrl = "https://openapi.alipay.com/gateway.do";
$c->appId = "app_id";
$c->rsaPrivateKey = '请填写开发者私钥去头去尾去回车，一行字符串' ;
$c->format = "json";
$c->charset = "GBK";
$c->signType= "RSA2";
$c->alipayrsaPublicKey = '请填写支付宝公钥，一行字符串';
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.user.userinfo.share
$request= new AlipayUserUserinfoShareRequest();
//授权类接口执行API调用时需要带上accessToken
$response= $c->execute($request,"accessToken");
```

### 用户授权接口调用示例（证书）
```php
$c = new AopCertClient;
$appCertPath = "应用证书路径（要确保证书文件可读），例如：/home/admin/cert/appCertPublicKey.crt";
$alipayCertPath = "支付宝公钥证书路径（要确保证书文件可读），例如：/home/admin/cert/alipayCertPublicKey_RSA2.crt";
$rootCertPath = "支付宝根证书路径（要确保证书文件可读），例如：/home/admin/cert/alipayRootCert.crt";
$c->gatewayUrl = "https://openapi.alipay.com/gateway.do";
$c->appId = "app_id";
$c->rsaPrivateKey = '请填写开发者私钥去头去尾去回车，一行字符串' ;
$c->format = "json";
$c->charset = "GBK";
$c->signType= "RSA2";
//调用getPublicKey从支付宝公钥证书中提取公钥
$c->alipayrsaPublicKey = $c->getPublicKey($alipayCertPath);
//是否校验自动下载的支付宝公钥证书，如果开启校验要保证支付宝根证书在有效期内
$c->isCheckAlipayPublicCert = true;
//调用getCertSN获取证书序列号
$c->appCertSN = $c->getCertSN($appCertPath);
//调用getRootCertSN获取支付宝根证书序列号
$c->alipayRootCertSN = $c->getRootCertSN($rootCertPath);
//实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.user.userinfo.share
$request= new AlipayUserUserinfoShareRequest();
//授权类接口执行API调用时需要带上accessToken
$response= $c->execute($request,"accessToken");
```

### 应用授权接口调用示例（ISV 代理商家调用）
```php
$c = new AopClient;
$c->gatewayUrl = "https://openapi.alipay.com/gateway.do";
$c->appId = "app_id";
$c->rsaPrivateKey = '请填写开发者私钥去头去尾去回车，一行字符串' ;
$c->format = "json";
$c->charset = "GBK";
$c->signType= "RSA2";
$c->alipayrsaPublicKey = '请填写支付宝公钥，一行字符串';
## 实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify
$request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
$request->bizContent = "{" .
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," .
"    \"primary_industry_code\":\"10001/20102\"," .
"    \"secondary_industry_code\":\"10001/20102\"," .
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" .
"  }";
//ISV代理商家调用需要传入app_auth_token
$response= $c->execute($request,NULL,"app_auth_token");
```

### 应用授权接口调用示例（ISV 代理商家调用）（证书）
```php
$c = new AopCertClient;
$appCertPath = "应用证书路径（要确保证书文件可读），例如：/home/admin/cert/appCertPublicKey.crt";
$alipayCertPath = "支付宝公钥证书路径（要确保证书文件可读），例如：/home/admin/cert/alipayCertPublicKey_RSA2.crt";
$rootCertPath = "支付宝根证书路径（要确保证书文件可读），例如：/home/admin/cert/alipayRootCert.crt";
$c->gatewayUrl = "https://openapi.alipay.com/gateway.do";
$c->appId = "app_id";
$c->rsaPrivateKey = '请填写开发者私钥去头去尾去回车，一行字符串' ;
$c->format = "json";
$c->charset = "GBK";
$c->signType= "RSA2";
//调用getPublicKey从支付宝公钥证书中提取公钥
$c->alipayrsaPublicKey = $c->getPublicKey($alipayCertPath);
//是否校验自动下载的支付宝公钥证书，如果开启校验要保证支付宝根证书在有效期内
$c->isCheckAlipayPublicCert = true;
//调用getCertSN获取证书序列号
$c->appCertSN = $c->getCertSN($appCertPath);
//调用getRootCertSN获取支付宝根证书序列号
$c->alipayRootCertSN = $c->getRootCertSN($rootCertPath);
## 实例化具体API对应的request类,类名称和接口名称对应,当前调用接口名称：alipay.open.public.template.message.industry.modify
$request = new AlipayOpenPublicTemplateMessageIndustryModifyRequest();
//SDK已经封装掉了公共参数，这里只需要传入业务参数
//此次只是参数展示，未进行字符串转义，实际情况下请转义
$request->bizContent = "{" .
"    \"primary_industry_name\":\"IT科技/IT软件与服务\"," .
"    \"primary_industry_code\":\"10001/20102\"," .
"    \"secondary_industry_code\":\"10001/20102\"," .
"    \"secondary_industry_name\":\"IT科技/IT软件与服务\"" .
"  }";
//ISV代理商家调用需要传入app_auth_token
$response= $c->execute($request,NULL,"app_auth_token");
```
