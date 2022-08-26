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

A：报错“ISV 权限不足”是由于未添加获取会员手机号功能包。请至小程序管理后台添加功能包。

1. 在 [开放平台控制台](https://openhome.alipay.com/dev/workspace) 的 **功能列表** 中，点击 **添加功能**。

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/9219534cf0b476cb9654aa6dfcafcaff.png#align=left&display=inline&height=105&margin=%5Bobject%20Object%5D&originHeight=212&originWidth=1500&status=done&style=stroke&width=746)

2. 添加 **获取会员手机号** 功能包。

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b543a501c7989411375fa111cfed2ca3.png#align=left&display=inline&height=331&margin=%5Bobject%20Object%5D&originHeight=456&originWidth=723&status=done&style=stroke&width=525)

3. 点击 **用户信息申请**。

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/22e7a6060e673a4129487a1b06da79d9.png?x-oss-process=image/resize,w_1500#align=left&display=inline&height=36&margin=%5Bobject%20Object%5D&originHeight=72&originWidth=1500&status=done&style=stroke&width=746)

4. 在 **申请权限** 中申请用户手机号。

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fc511f9394f5519a596e5aba336c2622.png#align=left&display=inline&height=87&margin=%5Bobject%20Object%5D&originHeight=170&originWidth=1456&status=done&style=stroke&width=746)

5. 填写申请原因、使用场景等信息，提交申请，等待审核。

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/0b2e295836fd49f1f63304ac802dcf90.png#align=left&display=inline&height=362&margin=%5Bobject%20Object%5D&originHeight=499&originWidth=752&status=done&style=none&width=546)

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
