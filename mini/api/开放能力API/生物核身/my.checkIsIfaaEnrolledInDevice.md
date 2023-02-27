# 简介
获取设备内是否录入如指纹等生物信息的接口。

## 使用限制

- 基础库 [2.8.1](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.3.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```java
if (my.canIUse('checkIsIfaaEnrolledInDevice')) {
  my.checkIsIfaaEnrolledInDevice({
    checkAuthMode: 'fingerPrint',
    success(res) {
      console.log(res.isEnrolled);
    },
    fail(res) {
      console.error(res);
    }
  });
}
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| checkAuthMode | String | 是 | 获取设备内是否录入如指纹等生物信息的接口。可选值：<ul><li>fingerPrint：指纹识别。</li><li>facial：人脸识别。</li></ul> |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |

### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| isEnrolled | Boolean | 是否已录入信息。 |
