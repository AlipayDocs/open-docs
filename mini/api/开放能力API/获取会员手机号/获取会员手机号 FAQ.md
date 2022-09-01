### Q：如何处理调用 my.getPhoneNumber，报错“无效的授权关系”？

A：

- 用户 **主动触发** 才能发起获取手机号请求，不能由 API 直接获取用户手机号，需使用 [button 组件](https://opendocs.alipay.com/mini/component/button) 的“点击”动作来触发操作。需要将 `<button>` 组件 `open-type` 的值设置为 `getAuthorize`，并将 `scope` 设置为 `phoneNumber` 。示例代码：

```html
<!-- .axml -->
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

- 当用户点击并同意之后，可以通过 `my.getPhoneNumber()` 接口获取到支付宝服务器返回的加密数据， 然后在第三方服务端结合签名算法和 AES 密钥进行解密获取手机号，方法可查看 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3)，若用户未授权，直接调用 `my.getPhoneNumber()` 接口，则无法返回正确信息。

#### 操作流程：

1. 将 button 组件 open-type 的值设置为 getAuthorize。

示例代码：

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

Button 属性说明：

| **属性**       | **说明**                                         |
| -------------- | ------------------------------------------------ |
| open-type      | 此处设置为 `getAuthorize`，用于授权。            |
| scope          | 此处设置为 `phoneNumber`，手机号码。             |
| onGetAuthorize | 授权成功回调（在回调里可以调用获取信息的接口）。 |
| onError        | 授权失败回调（包括用户拒绝和系统异常）。         |

2. 用户点击并同意授权后，可以通过 my.getPhoneNumber 获取到支付宝服务器返回的加密数据， 然后在第三方服务端结合签名算法和 AES 密钥进行解密获取手机号，方法可查看 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3)。

```javascript
my.getPhoneNumber({
  success: res => {
    let encryptedData = res.response;
    my.request({
      url: '你的服务端',
      data: encryptedData,
    });
  },
  fail: res => {
    console.log(res);
    console.log('getPhoneNumber_fail');
  },
});
```

### Q：如何处理调用 my.getPhoneNumber，报错“ISV 权限不足”？

A：报错“ISV 权限不足”是由于未添加获取会员手机号产品。

1. 进入 [开放平台控制台](https://open.alipay.com/develop/manage) 的 对应小程序详情页 > **产品绑定** 绑定 **获取会员手机号**。
![](https://cdn.nlark.com/yuque/0/2022/png/179989/1661931956108-d30527bc-ad74-4fc9-80ac-1b67c0a7e811.png)

2. 点击 **用户信息申请** 进入申请页面，点击 **申请权限** 申请用户手机号。
![](https://cdn.nlark.com/yuque/0/2022/png/179989/1661932190662-fdbdbe98-1a22-4c10-9afe-57fe87ca7a61.png)

3. 填写申请原因、使用场景等信息，提交申请，等待审核。
![](https://cdn.nlark.com/yuque/0/2022/png/179989/1660273140099-5e0209d3-7ee4-427a-b3f0-62bc006e309b.png?x-oss-process=image%2Fresize%2Cw_998)

### Q：如何处理返回错误码 20000/40001/40002/40003？

A：

| **错误码** | **错误详情** | **解决方案** |
| --- | --- | --- |
| 20000 | 系统繁忙 | 稍后再试。 |
| 40001 | 应用未设置默认签名类型 | 在 [开放平台控制台](https://openhome.alipay.com/dev/workspace) > **设置** > **开发设置** 中，设置 **支付宝公钥** 和 **应用网关**。 |
| 40002 | 加密异常 | 在 [开放平台控制台](https://openhome.alipay.com/dev/workspace) > **设置** > **开发设置** 中，设置 **aes 密钥**，aes 相关信息可查看 **接口内容加密方式**。 |
| 40003 | 无效的授权关系 | 用户未同意授权，或授权已失效，可稍后再试。 |

### Q：为何返回的数据是密钥和签名，并没有获取到手机号？

A：my.getPhoneNumber 获取的是支付宝服务器返回的加密数据。

在第三方服务端结合签名算法和 AES 密钥进行解密可获取手机号，方法可查看 **接口内容加密方式**。

服务端解密后的明文示例如下：

```json
{
  "code": "10000",
  "msg": "Success",
  "mobile": "18818181818"
}
```

### Q：获取用户手机号为何没有返回 sign？

A：请确保已设置支付宝公钥，aes 密钥、应用网关。若缺失这三个设置任一，在调用 my.getPhoneNumber 时可能只返回 response。
