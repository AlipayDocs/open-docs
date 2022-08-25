# 简介

设置截屏/录屏时的屏幕表现，仅支持在 Android 端调用。

## 使用限制

- 基础库 [2.7.13](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 进行系统截屏/录屏时隐藏屏幕
if (my.setVisualEffectOnCapture) {
  my.setVisualEffectOnCapture({
    visualEffect: 'hidden',
  });
}
// 正常使用系统截屏/录屏功能
if (my.setVisualEffectOnCapture) {
  my.setVisualEffectOnCapture({
    visualEffect: 'none',
  });
}
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| visualEffect | String | 否 | 截屏/录屏时的表现，仅支持 none / hidden，传入 hidden 则表示在截屏/录屏时隐藏屏幕。<br />默认值 none。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### visualEffect 合法值

| **值** | **说明**                      |
| ------ | ----------------------------- |
| none   | 正常使用系统截屏/录屏功能。   |
| hidden | 进行系统截屏/录屏时隐藏屏幕。 |
