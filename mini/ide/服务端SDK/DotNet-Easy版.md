
## 简介
适用于 .Net Framework 4.6.1、.Net Core 2.0 及其以上版本。

## 下载地址

- [NuGet 项目依赖](https://www.nuget.org/packages/AlipayEasySDK)
- [GitHub 项目主页](https://github.com/alipay/alipay-easysdk/tree/master/csharp)

## 示例代码

### 普通调用示例
```csharp
using System;
using Alipay.EasySDK.Factory;
using Alipay.EasySDK.Kernel;
using Alipay.EasySDK.Kernel.Util;
using Alipay.EasySDK.Payment.FaceToFace.Models;
namespace SDKDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. 设置参数（全局只需设置一次）
            Factory.SetOptions(GetConfig());
            try
            {
                // 2. 发起API调用（以创建当面付收款二维码为例）
                AlipayTradePrecreateResponse response = Factory.Payment.FaceToFace()
                    .PreCreate("Apple iPhone11 128G", "2234567234890", "5799.00");
                // 3. 处理响应或异常
                if (ResponseChecker.Success(response))
                {
                    Console.WriteLine("调用成功");
                }
                else
                {
                    Console.WriteLine("调用失败，原因：" + response.Msg + "，" + response.SubMsg);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("调用遭遇异常，原因：" + ex.Message);
                throw ex;
            }
        }
        static private Config GetConfig()
        {
            return new Config()
            {
                Protocol = "https",
                GatewayHost = "openapi.alipay.com",
                SignType = "RSA2",
                AppId = "<-- 请填写您的AppId，例如：2019091767145019 -->",
                // 为避免私钥随源码泄露，推荐从文件中读取私钥字符串而不是写入源码中
                MerchantPrivateKey = "<-- 请填写您的应用私钥，例如：MIIEvQIBADANB ... ... -->",
                MerchantCertPath = "<-- 请填写您的应用公钥证书文件路径，例如：/foo/appCertPublicKey_2019051064521003.crt -->",
                AlipayCertPath = "<-- 请填写您的支付宝公钥证书文件路径，例如：/foo/alipayCertPublicKey_RSA2.crt -->",
                AlipayRootCertPath = "<-- 请填写您的支付宝根证书文件路径，例如：/foo/alipayRootCert.crt -->",
                // 如果采用非证书模式，则无需赋值上面的三个证书路径，改为赋值如下的支付宝公钥字符串即可
                // AlipayPublicKey = "<-- 请填写您的支付宝公钥，例如：MIIBIjANBg... -->"
                //可设置异步通知接收服务地址（可选）
                NotifyUrl = "<-- 请填写您的支付类接口异步通知接收服务地址，例如：https://www.test.com/callback -->",
                //可设置AES密钥，调用AES加解密相关接口时需要（可选）
                EncryptKey = "<-- 请填写您的AES密钥，例如：aa4BtZ4tspm2wnXLb1ThQA== -->"
            };
        }
    }
}
```

### 第三方代理调用示例
```csharp
Factory.Payment.FaceToFace()
    //调用Agent扩展方法，设置app_auth_token，完成ISV代调用
    .Agent("ca34ea491e7146cc87d25fca24c4cD11")
    .PreCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```

### 设置独立的异步通知地址示例
```csharp
Factory.Payment.FaceToFace()
    // 调用AsyncNotify扩展方法，可以为每此API调用，设置独立的异步通知地址
    // 此处设置的异步通知地址的优先级高于全局Config中配置的异步通知地址
    .AsyncNotify("https://www.test.com/callback")
    .PreCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```

### 支付类异步通知验签示例
```csharp
Dictionary<string, string> parameters = new Dictionary<string, string>
{
    { "charset", "UTF-8" },
    { "sign", "GM0CbuqaEivqgb......" },
    { "app_id", "2018091261392200" },
    { "sign_type", "RSA2" },
    { "isv_ticket", "" },
    { "timestamp", "2020-03-25 16:27:08" }
    //... ...接收到的所有参数放入一个Map中
};
Factory.Payment.Common().VerifyNotify(parameters);
```

### 动态扩展 SDK 功能满足个性化需求
当 SDK 的 API 声明中的参数不满足个性化需求时，可按如下方式追加可选业务参数：
```csharp
Dictionary<string, object> goodsDetail = new Dictionary<string, object>
{
    { "goods_id", "apple-01" },
    { "goods_name", "Apple iPhone11 128G" },
    { "quantity", 1 },
    { "price", "5799.00" }
};
goodsDetailList.Add(goodsDetail);
Factory.Payment.FaceToFace()
    // 调用optional扩展方法，完成可选业务参数（biz_content下的可选字段）的设置
    .Optional("seller_id", "2088102146225135")
    .Optional("discountable_amount", "8.88")
    .Optional("goods_detail", goodsDetailList)
    .PreCreate("Apple iPhone11 128G", "2234567890", "5799.00");
Dictionary<string, object> optionalArgs = new Dictionary<string, object>
{
    { "seller_id", "2088102146225135" },
    { "discountable_amount", "8.88" },
    { "goods_detail", goodsDetailList }
};
Factory.Payment.FaceToFace()
    // 也可以调用batchOptional扩展方法，批量设置可选业务参数（biz_content下的可选字段）
    .BatchOptional(optionalArgs)
    .PreCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```
当想要调用的 OpenAPI 在 SDK 中没有对应的 API 与之对应时，可按如下方式调用 OpenAPI：<br />**注意**：文件上传类 OpenAPI、生成字符串类的 OpenAPI（老版 SDK 中需使用 sdkExecute）、生成 Form 表单类的 OpenAPI（老版 SDK 中需要使用 pageExecute）本调用方式暂不支持。
```csharp
//设置系统参数（OpenAPI中非biz_content里的参数）
Dictionary<string, string> textParams = new Dictionary<string, string>
{
    { "app_auth_token", "201712BB_D0804adb2e743078d1822d536956X34" }
};
//设置业务参数（OpenAPI中biz_content里的参数）
Dictionary<string, object> bizParams = new Dictionary<string, object>
{
    { "subject", "Iphone6 16G" },
    { "out_trade_no", Guid.NewGuid().ToString() },
    { "total_amount", "0.10" },
    { "buyer_id", "2088002656718920" }
};
Dictionary<string, string> extendParams = new Dictionary<string, string>
{
    { "hb_fq_num", "3" },
    { "hb_fq_seller_percent", "3" }
};
bizParams.Add("extend_params", extendParams);
Factory.Util.Generic().Execute("alipay.trade.create", textParams, bizParams);
```

<br />

