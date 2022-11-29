# 简介

**my.getPhoneNumber** 获取支付宝用户绑定的手机号。

## 使用限制

- 此 API 暂仅支持企业支付宝小程序使用。
- 请妥善保管和谨慎使用所获取的用户手机号，如有超出约定范围等不合理使用的情况，支付宝将永久回收接口权限。

## 必读指南

通过 my.getPhoneNumber 获取用户手机号，请按以下步骤进行：

### 第一步：设置接口内容加密方式

在 [开放平台控制台](https://open.alipay.com/develop/mini/sub/dev-setting?bundleId=com.alipay.alipaywallet) 设置 **接口内容加密方式**（可参考文档 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3) ）。**未设置接口加密方式而直接调用 my.getPhoneNumber，将得到异常响应“缺少加密配置”（code 40001）**。如需 [验证内容的真实性](https://opendocs.alipay.com/common/02mriz)，请参考文档 [接口加签方式] 在 (https://opendocs.alipay.com/common/02mriz) 设置 **接口加签方式（密钥/证书）**。

### 第二步：绑定产品并申请用户信息

在开放平台控制台为当前小程序绑定 [获取会员手机号](https://open.alipay.com/develop/uni/mini/choose-product?bundleId=com.alipay.alipaywallet&productCode=I1080300001000046451) 产品，并进行<a href="https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*ZRjrQ4XnXcQAAAAAAAAAAAAAARQnAQ" target="_blank">用户信息申请</a>（需**登录主账号或管理员账号**才能看到此入口）。如果`申请用户信息`灰色不可点击，请对照 [用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu) 检查小程序的主营行业设置。**未绑定获取会员手机号产品或未通过用户信息申请直接调用 my.getPhoneNumber，解密后将得到异常响应“ISV权限不足”（code 40006）**。

### 第三步：获取用户授权后调用 my.getPhoneNumber

参考后文示例代码，使用 `open-type` 为 `getAuthorize`、`scope` 为 `phoneNumber` 的 [`<button>` 组件](https://opendocs.alipay.com/mini/component/button)，在 `<button>` 的 `onGetAuthorize`（用户同意授权）事件中调用 my.getPhoneNumber，并恰当处理 `onError`（用户拒绝授权）事件。**未经用户授权而直接调用 my.getPhoneNumber，解密后将得到异常响应“无效的授权关系”（code 40003）**。

### 第四步：服务端解密和验签

将 my.getPhoneNumber 返回的 `response` 字段发送给服务端，参考 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3) 进行验签解密。如果第一步中没有设置**接口加签方式**，response 中将不会有 sign 字段，请跳过验签步骤。如果第二步或第三步未正确完成，报错信息也会在此解密步骤完成后才能看到。如果一切正常，解密得到的 JSON 内容 mobile 字段即为手机号（参见后文**服务端解密结果示例**）。


# 接口调用

## 示例代码

### .axml 示例代码

```html
<button
  open-type="getAuthorize"
  scope="phoneNumber"
  onGetAuthorize="getPhoneNumber"
  onError="handleAuthError"
>
  授权手机号
</button>
```

### .js 示例代码

```javascript
Page({
  getPhoneNumber() {
    my.getPhoneNumber({
      success: (res) => {
        my.request({
          method: 'POST',
          url: 'https://your-server-address', // 替换成自己的服务端地址
          data: res.response,
          success: (res) => {
            my.alert({
              title: 'getPhoneNumber 解密结果',
              content: JSON.stringify(res.data),
            });  
          },
          fail: (res) => {
            my.alert({
              title: 'getPhoneNumber 解密失败',
              content: JSON.stringify(res),
            });  
          }
        });
      },
      fail: (res) => {
        my.alert({
          title: 'getPhoneNumber 失败',
          content: JSON.stringify(res),
        });
      }
    });
  },
  handleAuthError(e) {
    my.alert({ title: '用户拒绝授权', content: JSON.stringify(e.detail) });
  }
});
```

### 服务端解密代码

以下为 java 示例。其他语言请参考 [服务器端各语言实现手机号/运动步数-AES密文解密](https://opendocs.alipay.com/support/01rb0s)。

```java
import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.TypeReference;
import com.alibaba.fastjson.parser.Feature;
import com.alipay.api.AlipayApiException;
import com.alipay.api.internal.util.AlipayEncrypt;
import com.alipay.api.internal.util.AlipaySignature;
import java.util.Map;

// 读取小程序前端发来的加密信息
String response = "....";

// 1. 获取验签和解密所需要的参数
Map<String, String> openapiResult = JSON.parseObject(response,new TypeReference<Map<String, String>>() {}, Feature.OrderedField);
String signType = "RSA2";
String charset = "UTF-8";
String encryptType = "AES";
String sign = openapiResult.get("sign");
String content = openapiResult.get("response");

// 判断是否为加密内容
boolean isDataEncrypted = !content.startsWith("{");
boolean signCheckPass = false;

// 2. 验签
String signVeriKey = "..."; // 小程序对应的支付宝公钥
String signContent = content;
// 如果是加密的报文则需要在密文的前后添加双引号
if (isDataEncrypted) {    
  signContent = "\"" + signContent + "\"";
} 

try {    
  signCheckPass = AlipaySignature.rsaCheck(signContent, sign, signVeriKey, charset, signType);
} catch (AlipayApiException e) {    
  // 验签异常, 日志
} 

if (!signCheckPass) {   
  //验签不通过（异常或者报文被篡改），终止流程（不需要做解密）    
  throw new Exception("验签失败");
}

// 3. 解密
String decryptKey = "..."; // 小程序对应的 AES 密钥
String plainData = null;
if (isDataEncrypted) {    
  try {        
    plainData = AlipayEncrypt.decryptContent(content, encryptType, decryptKey, charset);    
  } catch (AlipayApiException e) {       
    //解密异常, 记录日志       
    throw new Exception("解密异常");   
  }
} else {    
  plainData = content;
}
```

## 服务端解密结果示例

```javascript
// 正常结果
{
  "code": "10000",
  "msg": "Success",
  "mobile": "1597671905"
}

// 异常结果。解决方案：请参考接入必读第一步
{
  "code": "40001",
  "msg": "Missing Required Arguments",
  "subCode": "isv.missing-encrypt-key",
  "subMsg": "缺少加密配置"
}

// 异常结果。解决方案：请参考接入必读第一步
{
  "code": "40006", // 解决方案：请参考接入必读第二步
  "msg": "Insufficient Permissions",
  "subCode": "isv.insufficient-isv-permissions",
  "subMsg": "ISV权限不足，建议在开发者中心检查对应功能是否已经添加，解决办法详见：https:\/\/docs.open.alipay.com\/common\/isverror"
}

// 异常结果。解决方案：请参考接入必读第一步
{
  "code": "40003", // 解决方案：请参考接入必读第三步
  "msg": "Insufficient Conditions",
  "subCode": "isv.invalid-auth-relations",
  "subMsg": "无效的授权关系"
}

// 异常结果。解决方案：请参考接入必读第一步
{
  "code": "20000", // 解决方案：请稍后重试
  "msg": "Service Currently Unavailable",
  "subCode": "aop.unknow-error",
  "subMsg": "系统繁忙"
}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 出参

success 回调会携带一个 Object 类型的对象，其参数如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| response | String | 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理。 |

# 常见问题 FAQ

## Q：调用 my.getPhoneNumber，报错 “缺少加密配置”，如何处理？

A：请参考本文**接入必读**部分第一步。

## Q：调用 my.getPhoneNumber 成功，但服务端解密后得到异常结果 “ISV 权限不足”，如何处理？

A：请参考本文**接入必读**部分第三步。

## Q：调用 my.getPhoneNumber 成功，但服务端解密后得到异常结果 “无效的授权关系”，如何处理？

A：请参考本文**接入必读**部分第三步。也可通过 [my.getSetting](https://opendocs.alipay.com/mini/api/xmk3ml) success 回调参数的 phoneNumber 字段判断用户是否授权过手机号，为 true 即已授权。

## Q：调用 my.getPhoneNumber 并成功解密，为什么得到的 mobile 字段为空？

A：一般为当前登录的支付宝账号没有绑定手机号所致。用户可通过 [账号管理页面](https://custweb.alipay.com/account/index.htm) 绑定手机号。
