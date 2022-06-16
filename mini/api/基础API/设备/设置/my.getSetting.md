# 简介
**my.getSetting** 是获取用户的当前设置的 API，返回值中只会出现小程序已经向用户请求过的权限。

## 使用限制

- 基础库 [1.8.0](https://opendocs.alipay.com/mini/framework/lib)  或更高版本；支付宝客户端  10.1.10 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
my.getSetting({
  success: (res) => {
    /*
     * res.authSetting = {
     *   "location": true,
     *   "audioRecord": true,
     *   ...
     * }
     */
  }
})
```

## 返回示例

### success 回调返回示例

执行成功时，触发 success 回调，回调参数示例如下：

```json
{
    "authSetting": {
        "camera": true,
        "location": true,
        "alipaysports": true,
        "aliaddress": true,
        "album": true,
        "userInfo": true,
        "phoneNumber": true
    }
}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| authSetting | Object | 用户授权结果，其中 key 为 scope 值，value 为 Boolean 值，表示用户是否允许授权，可查看 **scope 列表**。 |

### scope 列表
| **scope** | **对应接口** | **描述** |
| --- | --- | --- |
| location | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 地理位置。 |
| album | [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage)<br />[my.saveImage](https://opendocs.alipay.com/mini/api/media/image/my.saveimage) | 保存到相册。 |
| camera | [my.scan](https://opendocs.alipay.com/mini/api/scan) | 摄像头。 |
| alipaysports | [my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v) | 运动数据。 |
| phoneNumber | [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber) | 手机号码。 |
| aliaddress | [my.getAddress](https://opendocs.alipay.com/mini/api/lymgfk) | 收货地址。 |
| userInfo | [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) | 唤起授权界面，用户可以授权小程序获取支付宝会员的基础信息 。 |

# 常见问题 FAQ

## Q：my.getAuthCode 的授权关系可以通过 my.getSetting 接口查询吗？
A：不可以。[my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) 接口的授权关系可以查询。