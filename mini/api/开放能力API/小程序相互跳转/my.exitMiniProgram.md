# 简介

**my.exitMiniProgram** 退出当前小程序。必须有点击行为才能调用成功。

## 使用限制

- 基础库 [2.7.15](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 不支持在插件内调用。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码

```html
<button size="default" onTap="exitMiniProgram">exitMiniProgram</button>
```

### .js 示例代码

```javascript
Page({
  onReady() {
    my.exitMiniProgram({
      fail(res) {
        // 没有点击my.exitMiniProgram不会调用成功
        console.log(res);
      },
    });
  },
  exitMiniProgram(e) {
    // 如果成功退出小程序，会直接杀掉小程序进程，一般情况已经来不及执行success/complete回调。
    my.exitMiniProgram();
  },
});
```

## 参数

Object 类型，属性如下：

| **参数** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
