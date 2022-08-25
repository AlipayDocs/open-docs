# 简介

**my.openSetting** 是打开小程序设置界面的 API。返回用户权限设置的结果；设置界面只会出现小程序已经向用户请求过的权限。

## 使用限制

- 基础库 [1.8.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.10 或更高版本，若版本较低，建议采取  [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.openSetting({
  success: res => {
    /*
     * res.authSetting = {
     *   "userInfo": true,
     *   "location": true,
     *   ...
     * }
     */
  },
});
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
| authSetting | Object | 用户授权结果，其中 key 为 scope 值，value 为 Bool 值，表示用户是否允许授权，可查看 **scopes 列表**。 |

## scopes 列表

| **scopes** | **对应接口** | **描述** |
| --- | --- | --- |
| location | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 地理位置。 |
| album | [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage)<br />[my.saveImage](https://opendocs.alipay.com/mini/api/media/image/my.saveimage) | 保存到相册。 |
| camera | [my.scan](https://opendocs.alipay.com/mini/api/scan) | 摄像头。 |
| userInfo | [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) | 唤起授权界面，用户可以授权小程序获取支付宝会员的基础信息。 |
