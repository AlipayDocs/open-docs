
## 简介
适用于 JDK 1.8 及其以上版本的开发环境。
**注意：**需使用 maven 依赖引入，请勿直接下载 jar 包导入项目。

## 下载地址

- [Maven 项目依赖](https://mvnrepository.com/artifact/com.alipay.sdk/alipay-easysdk)
- [GitHub 项目主页](https://github.com/alipay/alipay-easysdk/tree/master/java)

## 示例代码

### 普通调用示例
```java
import com.alipay.easysdk.factory.Factory;
import com.alipay.easysdk.factory.Factory.Payment;
import com.alipay.easysdk.kernel.Config;
import com.alipay.easysdk.kernel.util.ResponseChecker;
import com.alipay.easysdk.payment.facetoface.models.AlipayTradePrecreateResponse;

public class Main {
    public static void main(String[] args) throws Exception {
        // 1. 设置参数（全局只需设置一次）
        Factory.setOptions(getOptions());
        try {
            // 2. 发起API调用（以创建当面付收款二维码为例）
            AlipayTradePrecreateResponse response = Payment.FaceToFace()
                    .preCreate("Apple iPhone11 128G", "2234567890", "5799.00");
            // 3. 处理响应或异常
            if (ResponseChecker.success(response)) {
                System.out.println("调用成功");
            } else {
                System.err.println("调用失败，原因：" + response.msg + "，" + response.subMsg);
            }
        } catch (Exception e) {
            System.err.println("调用遭遇异常，原因：" + e.getMessage());
            throw new RuntimeException(e.getMessage(), e);
        }
    }

    private static Config getOptions() {
        Config config = new Config();
        config.protocol = "https";
        config.gatewayHost = "openapi.alipay.com";
        config.signType = "RSA2";

        config.appId = "<-- 请填写您的AppId，例如：2019091767145019 -->";

        // 为避免私钥随源码泄露，推荐从文件中读取私钥字符串而不是写入源码中
        config.merchantPrivateKey = "<-- 请填写您的应用私钥，例如：MIIEvQIBADANB ... ... -->";

        //注：证书文件路径支持设置为文件系统中的路径或CLASS_PATH中的路径，优先从文件系统中加载，加载失败后会继续尝试从CLASS_PATH中加载
        config.merchantCertPath = "<-- 请填写您的应用公钥证书文件路径，例如：/foo/appCertPublicKey_2019051064521003.crt -->";
        config.alipayCertPath = "<-- 请填写您的支付宝公钥证书文件路径，例如：/foo/alipayCertPublicKey_RSA2.crt -->";
        config.alipayRootCertPath = "<-- 请填写您的支付宝根证书文件路径，例如：/foo/alipayRootCert.crt -->";

        //注：如果采用非证书模式，则无需赋值上面的三个证书路径，改为赋值如下的支付宝公钥字符串即可
        // config.alipayPublicKey = "<-- 请填写您的支付宝公钥，例如：MIIBIjANBg... -->";

        //可设置异步通知接收服务地址（可选）
        config.notifyUrl = "<-- 请填写您的支付类接口异步通知接收服务地址，例如：https://www.test.com/callback -->";

        //可设置AES密钥，调用AES加解密相关接口时需要（可选）
        config.encryptKey = "<-- 请填写您的AES密钥，例如：aa4BtZ4tspm2wnXLb1ThQA== -->";

        return config;
    }
}
```



### 第三方代理调用示例
```java
Factory.Payment.FaceToFace()
    // 调用agent扩展方法，设置app_auth_token，完成第三方代调用
    .agent("ca34ea491e7146cc87d25fca24c4cD11")
    .preCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```

### 设置独立的异步通知地址示例
```java
Factory.Payment.FaceToFace()
    // 调用asyncNotify扩展方法，可以为每次API调用，设置独立的异步通知地址
    // 此处设置的异步通知地址的优先级高于全局Config中配置的异步通知地址
    .asyncNotify("https://www.test.com/callback")
    .preCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```

### 支付类异步通知验签示例
```java
Map<String, String> parameters = new HashMap<>();
parameters.put("charset", "UTF-8");
parameters.put("sign", "GM0CbuqaEivqgb......");
parameters.put("app_id", "2018091261392200");
parameters.put("sign_type", "RSA2");
parameters.put("isv_ticket", "");
parameters.put("timestamp", "2020-03-25 16:27:08");
//... ... 接收到的所有参数放入一个Map中
Factory.Payment.Common().verifyNotify(parameters);
```

### 动态扩展 SDK 功能满足个性化需求
当 SDK 的 API 声明中的参数不满足个性化需求时，可按如下方式追加可选业务参数：
```java
List<Object> goodsDetailList = new ArrayList<>();
Map<String, Object> goodsDetail = new HashMap<>();
goodsDetail.put("goods_id", "apple-01");
goodsDetail.put("goods_name", "Apple iPhone11 128G");
goodsDetail.put("quantity", 1);
goodsDetail.put("price", "5799.00");
goodsDetailList.add(goodsDetail);

Factory.Payment.FaceToFace()
    // 调用optional扩展方法，完成可选业务参数（biz_content下的可选字段）的设置
    .optional("seller_id", "2088102146225135")
    .optional("discountable_amount", "8.88")
    .optional("goods_detail", goodsDetailList)
    .preCreate("Apple iPhone11 128G", "2234567890", "5799.00");


Map<String, Object> optionalArgs = new HashMap<>();
optionalArgs.put("seller_id", "2088102146225135");
optionalArgs.put("discountable_amount", "8.88");
optionalArgs.put("goods_detail", goodsDetailList);

Factory.Payment.FaceToFace()
    // 也可以调用batchOptional扩展方法，批量设置可选业务参数（biz_content下的可选字段）
    .batchOptional(optionalArgs)
    .preCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```
当想要调用的 OpenAPI 在 SDK 中没有对应的 API 与之对应时，可按如下方式调用 OpenAPI：<br />注意：文件上传类 OpenAPI、生成字符串类的 OpenAPI（老版 SDK 中需使用 sdkExecute）、生成 Form 表单类的 OpenAPI（老版 SDK 中需要使用 pageExecute）本调用方式暂不支持。
```java
//设置系统参数（OpenAPI中非biz_content里的参数）
Map<String, String> textParams = new HashMap<>();
textParams.put("app_auth_token", "201712BB_D0804adb2e743078d1822d536956X34");

//设置业务参数（OpenAPI中biz_content里的参数）
Map<String, Object> bizParams = new HashMap<>();
bizParams.put("subject", "Iphone6 16G");
bizParams.put("out_trade_no", UUID.randomUUID().toString());
bizParams.put("total_amount", "0.10");
bizParams.put("buyer_id", "2088002656718920");
Map<String, String> extendParams = new HashMap<>();
extendParams.put("hb_fq_num", "3");
extendParams.put("hb_fq_seller_percent", "3");
bizParams.put("extend_params", extendParams);

AlipayOpenApiGenericResponse response = Factory.Util.Generic().execute(
        "alipay.trade.create", textParams, bizParams);
```

<br />
<br />

