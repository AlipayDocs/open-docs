# 简介

**my.getPhoneNumber** 是获取支付宝用户绑定的手机号的 API。

my.getPhoneNumber 并非直接返回用户手机号，接入过程请参考下文**接入必读**一步步进行。

## 使用限制

- 此 API 暂仅支持企业支付宝小程序使用。
- 请妥善保管和谨慎使用所获取的用户手机号，如有超出约定范围等不合理使用的情况，支付宝有权针性永久回收接口权限。

## 接入必读

通过 my.getPhoneNumber 获取用户手机号的整体流程如下：

### 第一步：设置接口内容加密方式

- 在 [开放平台控制台](https://open.alipay.com/develop/mini/sub/dev-setting?bundleId=com.alipay.alipaywallet) 设置 **接口内容加密方式**（可参考文档 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3) ）。**未设置接口加密方式而直接调用 my.getPhoneNumber，会收到报错“缺少加密配置”（code 40001）**。

### 第二步：绑定产品并申请用户信息

- 到开放平台控制台为当前小程序绑定 [获取会员手机号](https://open.alipay.com/develop/uni/mini/choose-product?bundleId=com.alipay.alipaywallet&productCode=I1080300001000046451) 产品，并进行<a href="https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*ZRjrQ4XnXcQAAAAAAAAAAAAAARQnAQ" target="_blank">用户信息申请</a>（需登录主账号或管理员账号进行操作）。如果申请用户信息按钮为灰色，请对照 [用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu) 检查小程序的主营行业设置。**未绑定获取会员手机号产品或未通过用户信息申请直接调用 my.getPhoneNumber，返回内容经第四步服务端解密后将得到报错“ISV权限不足”（code 40006）**。

### 第三步：前端获取用户授权后并调用 my.getPhoneNumber

- 考示例代码，使用 open-type 为 getAuthorize、scope 为 phoneNumber 的 [`<button>` 组件](https://opendocs.alipay.com/mini/component/button)，由用户触发并完成授权，再在 onGetAuthorize 回调函数中调用 my.getPhoneNumber()。**未经用户授权而直接调用 my.getPhoneNumber，返回内容经第四步服务端解密后将得到报错“无效的授权关系”（code 40003）**。


### 第四步：服务端解密和验签

- 将 my.getPhoneNumber 返回的密文发送给服务端，[参考此文档进行解密](https://opendocs.alipay.com/common/02mse3)以获取手机号。如果上述第二步第三步未正确完成，报错信息也会在此解密步骤完成后才能看到。

- 【可选】如需 [验证加密内容的真实性](https://opendocs.alipay.com/common/02mriz)，请在 [开放平台控制台](https://open.alipay.com/develop/mini/sub/dev-setting?bundleId=com.alipay.alipaywallet) 设置 **接口加签方式（密钥/证书) **（可参考文档 [接口加签方式](https://opendocs.alipay.com/common/02mriz) ）。


# 接口调用

## 示例代码

### .axml 示例代码

```html
<button
  open-type="getAuthorize"
  onGetAuthorize="getPhoneNumber"
  onError="handleAuthError"
  scope="phoneNumber"
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
String decryptKey = "你的小程序对应的加解密密钥（为扩展考虑建议用appId+encryptType做密钥存储隔离）"; //如果是加密的报文则需要在密文的前后添加双引号
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

## 服务端解密结果示例

```javascript
// 正常结果
{
  "code": "10000",
  "msg": "Success",
  "mobile": "1597671905"
}

// 异常结果 1。解决方案：请参考接入必读第一步
{
  "code": "40001",
  "msg": "Missing Required Arguments",
  "subCode": "isv.missing-encrypt-key",
  "subMsg": "缺少加密配置"
}

// 异常结果 2。解决方案：请参考接入必读第一步
{
  "code": "40006", // 解决方案：请参考接入必读第二步
  "msg": "Insufficient Permissions",
  "subCode": "isv.insufficient-isv-permissions",
  "subMsg": "ISV权限不足，建议在开发者中心检查对应功能是否已经添加，解决办法详见：https:\/\/docs.open.alipay.com\/common\/isverror"
}

// 异常结果 3。解决方案：请参考接入必读第一步
{
  "code": "40003", // 解决方案：请参考接入必读第三步
  "msg": "Insufficient Conditions",
  "subCode": "isv.invalid-auth-relations",
  "subMsg": "无效的授权关系"
}

// 异常结果 4。解决方案：请参考接入必读第一步
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

## Q：“申请用户信息”为灰色不可点击，并提示 “所有用户信息字段都不满足申请条件”，如何处理？

A：检查小程序是否设置主营行业，并对照 [用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu) 检查应用是否符合主营行业及字段使用场景的要求。

## Q：调用 my.getPhoneNumber 返回的内容没有 sign 字段，如何处理？

A：请确保已设置支付宝公钥、AES 密钥、应用网关。这三者缺失其一，则在调用 my.getPhoneNumber 时将不带 sign 字段。

## Q：调用 my.getPhoneNumber 并成功解密，为什么得到的 mobile 字段为空？

A：一般为当前登录的支付宝账号没有绑定手机号所致。用户可通过 [账号管理页面](https://custweb.alipay.com/account/index.htm) 绑定手机号。
