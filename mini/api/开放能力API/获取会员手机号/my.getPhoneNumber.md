# 简介

**my.getPhoneNumber** 是获取支付宝用户绑定的手机号的 API。

获取用户手机号需要以下四步：

1. 设置 **接口内容加密方式**

- 此接口会返回加密后的用户手机号，请确保已完成接口内容加密方式配置：开放平台控制台 - [接口内容加密方式](https://open.alipay.com/develop/mini/sub/dev-setting?bundleId=com.alipay.alipaywallet)。参考文档 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3) 进行设置。
- 未设置接口加密方式直接调用此接口会返回：

```json
{
  "code": "40001",
  "msg": "Missing Required Arguments",
  "subCode": "isv.missing-encrypt-key",
  "subMsg": "缺少加密配置"
}
```

- 如果需要验证支付宝返回加密内容的真实性，请确保已在完成接口加签方式配置：开放平台控制台 - [接口加签方式（密钥/证书)](https://open.alipay.com/develop/mini/sub/dev-setting?bundleId=com.alipay.alipaywallet) 。参考文档 [接口加签方式](https://opendocs.alipay.com/common/02mriz) 进行设置。
- 未设置接口加签方式直接调用此接口将 **不会返回 sign 字段**。

2. 绑定 **获取会员手机号** 产品并 **申请用户信息**

- 使用此 API 请至开放平台控制台绑定 [获取会员手机号](https://open.alipay.com/develop/uni/mini/choose-product?bundleId=com.alipay.alipaywallet&productCode=I1080300001000046451) 产品，并登录主账号进行用户信息申请。 ![712x101](https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*ZRjrQ4XnXcQAAAAAAAAAAAAAARQnAQ)
- 如果申请用户信息按钮为灰色，请检查小程序是否设置主营行业，并且对照以下文档检查应用是否符合主营行业及字段使用场景的要求：[用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu)。
- 未绑定获取会员手机号产品或未进行用户信息申请直接调用此 API，返回内容解密后如下：

```json
{
  "code": "40006",
  "msg": "Insufficient Permissions",
  "subCode": "isv.insufficient-isv-permissions",
  "subMsg": "ISV权限不足，建议在开发者中心检查对应功能是否已经添加，解决办法详见：https://docs.open.alipay.com/common/isverror"
}
```

3. 用户授权

- 获取支付宝会员手机号需要用户进行授权，授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发， `<button>` 组件 `open-type` 的值设置为 `getAuthorize` 并将 `scope` 设为 `phoneNumber`。用户点击并同意之后，可以通过 `my.getPhoneNumber` 接口获取到支付宝会员加密后的手机号。
- 未经过 Button 授权直接调用此 API 会解密后会返回

```json
{
  "code": "40003",
  "msg": "Insufficient Conditions",
  "subCode": "isv.invalid-auth-relations",
  "subMsg": "无效的授权关系"
}
```

4、解密和验签

- 在服务端 [解密返回的密文获取手机号](https://opendocs.alipay.com/common/02mse3) 和 [验证加密内容的真实性](https://opendocs.alipay.com/common/02mriz)。

此功能需谨慎使用，若支付宝发现信息存在超出约定范围使用或者不合理使用等情况，支付宝有权永久回收该小程序的该接口权限。

## 使用限制

- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码

授权行为通过 `<button>` [组件](https://opendocs.alipay.com/mini/component/button) 的 **点击** 动作来触发。

唤起授权框，推荐兼容方案。

```html
<button
  a:if="{{canIUseAuthButton}}"
  open-type="getAuthorize"
  onGetAuthorize="onGetAuthorize"
  onError="onAuthError"
  scope="phoneNumber"
>
  授权手机号
</button>
```

### .js 示例代码

用户点击同意后，即可通过 my.getPhoneNumber() 获取用户绑定的手机号。

```javascript
data: {
  canIUseAuthButton: my.canIUse('button.open-type.getAuthorize')
},
onGetAuthorize(res) {
  my.getPhoneNumber({
    success: (res) => {
      let encryptedData = res.response;
      my.request({
        url: '你的后端服务端',
        data: encryptedData,
      });
    },
    fail: (res) => {
      console.log(res);
      console.log('getPhoneNumber_fail');
    },
  });
},
```

res.response 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理。更多语言的详细服务端处理流程可查看 [接口内容加解密方式](https://opendocs.alipay.com/common/02mse3)。

### Java 解密示例代码

```java
import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.TypeReference;
import com.alibaba.fastjson.parser.Feature;
import com.alipay.api.AlipayApiException;
import com.alipay.api.internal.util.AlipayEncrypt;
import com.alipay.api.internal.util.AlipaySignature;
import java.util.Map;

String response = "小程序前端返回的加密信息";

//1. 获取验签和解密所需要的参数
Map<String, String> openapiResult = JSON.parseObject(response,new TypeReference<Map<String, String>>() {}, Feature.OrderedField);
String signType = "RSA2";
String charset = "UTF-8";
String encryptType = "AES";
String sign = openapiResult.get("sign");
String content = openapiResult.get("response");

//判断是否为加密内容
boolean isDataEncrypted = !content.startsWith("{");
boolean signCheckPass = false;

//2. 验签
String signContent = content;
String signVeriKey = "你的小程序对应的支付宝公钥（为扩展考虑建议用appId+signType做密钥存储隔离）";
String decryptKey = "你的小程序对应的加解密密钥（为扩展考虑建议用appId+encryptType做密钥存储隔离）";//如果是加密的报文则需要在密文的前后添加双引号
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

//3. 解密
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

## 返回示例

服务端解密后的明文示例如下：

### 正常响应

```json
{
  "code": "10000",
  "msg": "Success",
  "mobile": "1597671905"
}
```

### 异常响应

```json
{
  "code": "40003",
  "msg": "Insufficient Conditions",
  "subCode": "isv.invalid-auth-relations",
  "subMsg": "无效的授权关系"
}
{
  "code": "20000",
  "msg": "Service Currently Unavailable",
  "subCode": "aop.unknow-error",
  "subMsg": "系统繁忙"
}
{
  "code": "40001",
  "msg": "Missing Required Arguments",
  "subCode": "isv.missing-encrypt-key",
  "subMsg": "缺少加密配置"
}
// 解决方案：开放平台开发设置配置接口内容加密方式
{
  "code": "40002",
  "msg": "Invalid Arguments",
  "subCode": "isv.invalid-encrypt",
  "subMsg": "加密异常"
}
// 解决方案：按文档重新设置AES密钥
{
  "code": "40006",
  "msg": "Insufficient Permissions",
  "subCode": "isv.insufficient-isv-permissions",
  "subMsg": "ISV权限不足，建议在开发者中心检查对应功能是否已经添加，解决办法详见：https:\/\/docs.open.alipay.com\/common\/isverror"
}
// 解决方案：开放平台控制台绑定获取会员手机号产品
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调会携带一个 Object 类型的对象，其参数如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| response | String | 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理。 |

# 常见问题 FAQ
## Q：调用 my.getPhoneNumber，报错 “无效的授权关系”，如何处理？

A：

- 用户 **主动授权** 后调用`my.getPhoneNumber` 才能获取用户支付宝会员的手机号。授权行为通过 `<button>` 组件的 **点击** 动作来触发操作，需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设为 `phoneNumber`。
- 可以通过 [my.getSetting](https://opendocs.alipay.com/mini/api/xmk3ml) 接口返回的 phoneNumber 判断用户是否授权过手机号，phoneNumber 为 true 即已授权。

## Q：调用 my.getPhoneNumber，报错 “缺少加密配置”，如何处理？

A：请先在开放平台控制台 - [接口加密方式](https://open.alipay.com/develop/mini/sub/dev-setting?bundleId=com.alipay.alipaywallet) 配置。详见文档 [接口内容加密方式](<(https://opendocs.alipay.com/common/02mse3)>)。

## Q：调用 my.getPhoneNumber 报错 “ISV 权限不足”，如何处理？

A：请检查小程序是否已绑定 **获取会员手机号** 并申请了 **用户信息**。若在产品绑定 [获取会员手机号](https://open.alipay.com/develop/uni/mini/choose-product?bundleId=com.alipay.alipaywallet&productCode=I1080300001000046451) 页面看不到用户信息申请的入口，请使用主账号登录，点击 **用户信息申请**。 ![|712x101](https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*ZRjrQ4XnXcQAAAAAAAAAAAAAARQnAQ)

## Q：申请用户信息不可点击并提示 “所有用户信息字段都不满足申请条件”，如何处理？

![|712x101](https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*RJn7TbMxO-wAAAAAAAAAAAAAARQnAQ) A：请检查小程序是否设置主营行业，并对照以下文档检查应用是否符合主营行业及字段使用场景的要求：[用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu)。

## Q：为什么调用 my.getPhoneNumber 返回的手机号为空？

A：一般情况下都是当前用户的支付宝账号没有绑定手机号所致，需要当前用户登录 [账号管理](https://custweb.alipay.com/account/index.htm)，绑定手机号。

### Q：获取用户手机号为何没有返回 sign？

A：请确保已设置支付宝公钥，aes 密钥、应用网关。若缺失这三个设置任一，在调用 my.getPhoneNumber 时可能只返回 response。
