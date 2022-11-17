# 文档地址
本文介绍支付宝小程序如何以技术方式接入支付宝卡包实现在小程序上 UID 发券，适用于已有小程序，需要技术接入的开发者。<br />UID 发券组件对接文档内容已整合至 **支付宝卡包**，请各位开发者根据 [支付宝卡包](https://opendocs.alipay.com/open/199/popvoucher) 指引进行开发接入。 

# 开发前准备
更多详情可查看 [小程序开发前准备](https://opendocs.alipay.com/support/01razz)。 

# 绑定产品

1. 创建应用后，在 **产品绑定** > **绑定产品** > 找到 **基础功能产品**，点击 **修改**。<br />![1.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/179989/1658391270885-f4e784b4-856f-4e75-908e-6fdcd2283fb2.jpeg#align=left&display=inline&height=499&margin=%5Bobject%20Object%5D&name=1.jpg&originHeight=998&originWidth=2268&size=276647&status=done&style=stroke&width=1134)
2. 在权限集中勾选 **支付宝卡包**，点击 **确定**。<br />![2-2.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/179989/1658396355088-d85b750a-3f01-451c-a82f-a729f2111175.jpeg#align=left&display=inline&height=542&margin=%5Bobject%20Object%5D&name=2-2.jpg&originHeight=1084&originWidth=2270&size=308993&status=done&style=none&width=1135)
3. 在选择产品页面，点击 **确定**，完成产品绑定。<br />![3.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/179989/1658391363749-dafd6166-bed2-42f7-adf2-ea79fa1d6ad6.jpeg#align=left&display=inline&height=506&margin=%5Bobject%20Object%5D&name=3.jpg&originHeight=1011&originWidth=2260&size=278703&status=done&style=stroke&width=1130)

# 创建卡包模板-发放卡包 

## 创建卡券模板
[alipay.pass.template.add](https://opendocs.alipay.com/open/02aila)（卡券模板创建接口）。<br />channelID 为小程序的 APPID。
```
/** 
* 新建模板 
* appAuthToken如服务商代替商家调用接口，需将商户授权后获取的app_auth_token带上；如商家自己调用，则传null。 
* bizContent 因该接口业务参数复杂，请查看接口文档 
*/ 
AlipayClient alipayClient = new DefaultAlipayClient("https://openapi.alipay.com/gateway.do", APP_ID, APP_PRIVATE_KEY, "json", CHARSET, ALIPAY_PUBLIC_KEY, "RSA2"); 
AlipayPassTemplateAddRequest request = new AlipayPassTemplateAddRequest();
request.putOtherTextParam("app_auth_token", appAuthToken); request.setBizContent(bizContent); 
AlipayPassTemplateAddResponse response=alipayClient.execute(request);
System.out.print(response.getBody());
//根据业务处理response
```
bizContent Json 串示例：
```json
String bizContent ="{"+ 
    "\"unique_id\":\"201807171147_PROD_T_A_002\"," //支付宝对该参数的请求有唯一性校验，请保证每次请求该参数唯一+ 
    "\"tpl_content\":" // tpl_content由content、icon、logo、strip 4 个元素构成+ 
        "{"+
            "\"logo\":\"https://alipass.alipay.com//temps/free/logo.png\"," // logo图片url地址，必传+
            "\"strip\":\"https://alipass.alipay.com//temps/free/strip.png\"," // 背景图片的url地址+
            "\"icon\\":\"http://alipassprod.test.alipay.net/temps/free/icon.png\"," // icon图片url地址+ 
            "\"content\":{" // 设计平台下载文件中 pass.json 内容，必传+ 
                "\"evoucherInfo\":{" // 基础属性+ 
                    "\"product\":\"free\","+ 
                    "\"einfo\":{"+ 
                        "\"logoText\\":\"3天\","+ 
                        "\"secondLogoText\":\"64场高清直播，进球就下红包雨\","+ 
                        "\"brandName\":\"上优酷，看世界杯\","+ 
                        "\"passImgRatio\":\"2.79\","+ 
                        "\"customFields\":[{"+ 
                            "\"more\":{"+ "\"url\":\"https://alipass.alipay.com//temps/free/logo.png\""+ "},"+ 
                            "\"label\":\"详细说明\","+ 
                            "\"type\":\"url\","+ 
                            "\"value\":\"\""+ 
                        "}],"+ 
                        "\"banner\":{"+ 
                            "\"bannerImg\":\"\","+ 
                            "\"url\":\"\""+ 
                        "},"+ 
                        "\"originPrice\":\"\","+
                        "\"passImg\":\"https://tfsimg.alipay.com/images/alipassprod/TB17fLOXB8rDuNk6Xejwu2EYXXa\","+ 
                        "\"auxiliaryFields\":[],"+ 
                        "\"useLimitDesc\":\"优酷VIP会员\""+ 
                   "},"+ 
                   "\"title\":\"测试优惠券\","+ 
                   "\"type\":\"marketVoucher\","+ 
                   "\"operation\":[{"+
                       "\"altText\":\"123456\","+ 
                       "\"format\":\"qrcode\","+ 
                       "\"messageEncoding\":\"UTF-8\","+ 
                       "\"message\":\"123456\""+ 
                   "}],"+ 
                   "\"endDate\":\"2099-07-23 12:22:22\","+ 
                   "\"startDate\":\"2019-07-22 12:22:22\""+ 
            "},"+ 
            "\"fileInfo\":{" // 文件属性+ "\"serialNumber\":\"$serialNumber$\","+ 
                "\"canShare\":true,"+ "\"formatVersion\":\"4\","+ 
                "\"canPresent\":false,"+ 
                "\"canBuy\":false"+ 
           "},"+ 
           "\"merchant\":{" // 商户属性+ "\"mname\":\"测试优惠券\","+ 
               "\"mcallbackUrl\":\"https://test.com/app/ali/coupon\""//此参数为商家发券网关地址+ "},"+
           "\"style\":{"+ 
               "\"backgroundColor\":\"RGB(255,126,0)\""+ 
           "},"+ 
           "\"source\":\"alipassprod\","+ 
           "\"platform\":{" // 渠道属性+ 
           "\"channelID\":\"2016091401912345\""+ 
           "}"+ 
    "}"+ 
  "}"+ 
"}";
```
**说明**：

- 模板中的自定义参数以双 $ 符号标志，即 $serialNumber$ 表示自定义参数名为 serialNumber，供发放卡券时使用。
- unique_id 参数支付宝有唯一性校验，请保证每次请求该值唯一。 

更多 bizContent 参数详情客户查看 [配置券模板内容](https://opendocs.alipay.com/open/016d5g)。 

## 小程序端跳转至领卡页面（ [UID 发券组件](https://opendocs.alipay.com/open/199/popvoucher)）

1. 替换下面连接的 templateId 和 userId 参数，获取 scheme 连接。<br />alipays://platformapi/startapp?appId=68687143&url=%2fwww%2fvoucher.html%3f__webview_options__%3dabv%253dNO%2526ttb%253dauto%26bizType%3dsvPage%26userId%3d20883024491795%26templateId%3d20180717115730423891234
2. 小程序端使用 my.ap.navigateToAlipayPage 跳转(打开)至领券前置页，页面唤起调用代码形如： <br />
```xml
my.ap.navigateToAlipayPage({    
    path:'alipays://platformapi/startapp?appId=68687143&url=%2fwww%2fvoucher.html%3f__webview_options__%3dabv%253dNO%2526ttb%253dauto%26bizType%3dsvPage%26userId%3d2088302449179665%26templateId%3d2018071711565730423891234',
    success:(res) => {        
        my.alert({content:'系统信息' + JSON.stringify(res)});
    },    
    fail:(error) => {        
        my.alert({content:'系统信息' + JSON.stringify(error)});            
            }})
```

## 用户点击领取后回调callback 地址
用户在发券确认页确认“领取并放入卡包”，页面将直接回调接口该接口进行发券操作。 callback url 回调的样例：
```
https://test.callback.com/alipay/callback.htm?templateId=2019041914323202306418702&userId=2088102124075657&token=b18ca3975872e092e5ded56a6e0884b9&timestamp=1559133415273
```
**注意**：地址必须为 HTTPS 协议，表单提交为 get 方法，同时返回商家发券结果，响应数据格式为 JSON。 

## 调用发券接口进行发券
[alipay.pass.instance.add](https://opendocs.alipay.com/open/02ailb)（卡券实例发放接口）。
```
/** 
* 发放卡券 
* appAuthToken 如服务商代替商家调用接口，需将商户授权后获取的app_auth_token带上；如商家自己调用，则传null。 
* bizContent 因该接口业务参数复杂，请详见接口文档  
*/ 
AlipayClient alipayClient = new DefaultAlipayClient("https://openapi.alipay.com/gateway.do", APP_ID, APP_PRIVATE_KEY, "json", CHARSET, ALIPAY_PUBLIC_KEY, "RSA2"); 
AlipayPassInstanceAddRequest request = new AlipayPassInstanceAddRequest(); request.putOtherTextParam("app_auth_token", appAuthToken); 
request.setBizContent(bizContent); 
AlipayPassInstanceAddResponse response = alipayClient.execute(request); 
System.out.print(response.getBody());
//根据业务处理response
```
bizContent Json 串示例：
```json
String bizContent = "{"+  
    "\"tpl_id\":\"2018071711565730423894319\","+ 
    "\"tpl_params\":{"+ 
        "\"expireTime\":\"2099-04-30 23:59:59\","+ 
        "\"activeTime\":\"2017-04-01 00:00:00\","+ 
        "\"serialNumber\":\"abc_test_201807171156\","+ 
        "\"url\":\"http://xxxxx\""+ 
        "},"+ 
    "\"recognition_type\":\"2\","+ 
    "\"recognition_info\":{"+ 
        "\"user_id\":\"2088302449179111\","+ 
        "\"user_token\":\"d81ca68b6811678960f1c7bd44791111\""+ 
    "}"+
"}";
```
**说明**： 

- tpl_params 中的 JSON 节点即为模板创建时设置的自定义参数（即模板中定义的 $xxxx$ ），每次发券可以自己定义内容，且其中的 serialNumber 支付宝有唯一性校验，每次请求请保证唯一性，不要重复。
- tpl_id：调用模板创建接口成功后返回模板 ID，该 ID 用于发放券票。
- recognition_info：支付宝用户识别信息： [UID 发券组件](https://opendocs.alipay.com/open/199/popvoucher) 或 [H5/小程序 UID 弹窗发券组件](https://opendocs.alipay.com/open/199/popvoucher#%E7%AC%AC%E4%B8%89%E6%AD%A5%EF%BC%9A%E7%94%A8%E6%88%B7%E8%B7%B3%E8%BD%AC%E8%87%B3%E9%A2%86%E5%88%B8%E9%A2%84%E8%A7%88%E9%A1%B5)。
- channelID：可设置为 APPID（从创建应用处获取）或者 PID。
- user_id：通过商户回调 callback 发券接口获得。
- user_token：即组件调用开发者在模板配置的 merchant.mcallbackUrl 接口，开发者在该接口 URL 的 query 参数中获取到的 token。
- 如出现“领券失败，请稍后重试”的报错信息，则表示 mcallbackUrl 响应格式错误，请参考 [正确的响应格式](https://opendocs.alipay.com/open/199/popvoucher)。
- recognition_type为1是通过交易号发券，目前已经不支持使用，请使用 recognition_type:2 。

