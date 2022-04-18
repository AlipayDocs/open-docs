## 简介
适用于 PHP 7.0 及其以上版本。

## 下载地址

- [Composer 项目依赖](https://packagist.org/packages/alipaysdk/easysdk)
- [GitHub 项目主页](https://github.com/alipay/alipay-easysdk/tree/master/php)

## 示例代码

### 普通调用示例
```php
<?php

require 'vendor/autoload.php';
use Alipay\EasySDK\Kernel\Factory;
use Alipay\EasySDK\Kernel\Config;

//1. 设置参数（全局只需设置一次）Factory::setOptions(getOptions());

try {
    //2. 发起API调用（以支付能力下的统一收单交易创建接口为例）
    $result = Factory::payment()->common()->create("iPhone6 16G", "20200326235526001", "88.88", "2088002656718920");
	
    //3. 处理响应或异常
    if (!empty($result->code) && $result->code == 10000) {
        echo "调用成功". PHP_EOL;
    } else {
        echo "调用失败，原因：". $result->msg."，".$result->sub_msg.PHP_EOL;
    }
} catch (Exception $e) {
    echo "调用失败，". $e->getMessage(). PHP_EOL;;
}

function getOptions()
{
    $options = new Config();
    $options->protocol = 'https';
    $options->gatewayHost = 'openapi.alipay.com';
    $options->signType = 'RSA2';
    
    $options->appId = '<-- 请填写AppId，例如：2019022663440152 -->';
    
    // 为避免私钥随源码泄露，推荐从文件中读取私钥字符串而不是写入源码中
    $options->merchantPrivateKey = '<-- 请填写应用私钥，例如：MIIEvQIBADANB ... ... -->';
    
    $options->alipayCertPath = '<-- 请填写支付宝公钥证书文件路径，例如：/foo/alipayCertPublicKey_RSA2.crt -->';
    $options->alipayRootCertPath = '<-- 请填写支付宝根证书文件路径，例如：/foo/alipayRootCert.crt" -->';
    $options->merchantCertPath = '<-- 请填写应用公钥证书文件路径，例如：/foo/appCertPublicKey_2019051064521003.crt -->';
    
    //注：如果采用非证书模式，则无需赋值上面的三个证书路径，改为赋值如下的支付宝公钥字符串即可
    // $options->alipayPublicKey = '<-- 请填写支付宝公钥，例如：MIIBIjANBg... -->';

    //可设置异步通知接收服务地址（可选）
    $options->notifyUrl = "<-- 请填写支付类接口异步通知接收服务地址，例如：https://www.test.com/callback -->";
    
    //可设置AES密钥，调用AES加解密相关接口时需要（可选）
    $options->encryptKey = "<-- 请填写AES密钥，例如：aa4BtZ4tspm2wnXLb1ThQA== -->";



    return $options;
}
```

### 第三方代理调用示例
```php
Factory::payment()->faceToFace()
    // 调用agent扩展方法，设置app_auth_token，完成ISV代调用
    ->agent("ca34ea491e7146cc87d25fca24c4cD11")
    ->preCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```

### 设置独立的异步通知地址示例
```php
Factory::payment()->faceToFace()
    // 调用asyncNotify扩展方法，可以为每此API调用，设置独立的异步通知地址
    // 此处设置的异步通知地址的优先级高于全局Config中配置的异步通知地址
    ->asyncNotify("https://www.test.com/callback")
    ->preCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```

### 支付类异步通知验签示例
```php
$parameters = array(
    "charset" => "UTF-8",
    "sign" => "GM0CbuqaEivqgb......",
    "app_id" => "2018091261392200",
    "sign_type" => "RSA2",
    "isv_ticket" => "",
    "timestamp" => "2020-03-25 16:27:08"
    //... ... 接收到的所有参数放入这里
);
Factory::payment()->common()->verifyNotify($parameters);
```

### 动态扩展 SDK 功能满足个性化需求
当 SDK 的 API 声明中的参数不满足个性化需求时，可按如下方式追加可选业务参数：
```php
$goodDetail = array(
            "goods_id" => "apple-01",
            "goods_name" => "iPhone6 16G",
            "quantity" => 1,
            "price" => "5799"
        );
        $goodsDetail[0] = $goodDetail;

Factory::payment()->faceToFace()
    // 调用optional扩展方法，完成可选业务参数（biz_content下的可选字段）的设置
    ->optional("seller_id", "2088102146225135")
    ->optional("discountable_amount", "8.88")
    ->optional("goods_detail", $goodsDetail)
    ->preCreate("Apple iPhone11 128G", "2234567890", "5799.00");


$optionalArgs = array(
            "timeout_express" => "10m",
            "body" => "Iphone6 16G"
        );

Factory::payment()->faceToFace()
    // 也可以调用batchOptional扩展方法，批量设置可选业务参数（biz_content下的可选字段）
    ->batchOptional($optionalArgs)
    ->preCreate("Apple iPhone11 128G", "2234567890", "5799.00");
```
当想要调用的 OpenAPI 在 SDK 中没有对应的 API 与之对应时，可按如下方式调用 OpenAPI：<br />**注意**：文件上传类 OpenAPI、生成字符串类的 OpenAPI（老版 SDK 中需使用 sdkExecute）、生成 Form 表单类的 OpenAPI（老版 SDK 中需要使用 pageExecute）本调用方式暂不支持。
```php
//设置系统参数（OpenAPI中非biz_content里的参数）
$textParams = array("app_auth_token" => "201712BB_D0804adb2e743078d1822d536956X34");

//设置业务参数（OpenAPI中biz_content里的参数）
$extendParams = array("hb_fq_num" => "3", "hb_fq_seller_percent" => "3");
$bizParams = array(
    "subject" => "Iphone6 16G",
    "out_trade_no" => microtime(),
    "total_amount" => "0.10",
    "buyer_id" => "2088002656718920",
    "extend_params" => $extendParams
);
Factory::util()->generic()->execute("alipay.trade.create",$textParams, $bizParams);

```

<br />

