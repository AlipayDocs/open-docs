# 简介
获取本机支持的 iFAA 生物认证方式。

## 使用限制

- 基础库 [2.8.1](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.3.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
if (my.canIUse('checkIsSupportIfaaAuthentication')) {
  my.checkIsSupportIfaaAuthentication({
    success(res) {
      console.log(res.supportMode);
    },
    fail(res) {
      console.error(res);
    }
  }) 
}
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |

### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| supportMode | Array/<String/> | 该设备支持的可被 IFAA 识别的生物识别方式。可选值：<ul><li>fingerPrint：指纹识别。</li><li>facial：人脸识别。</li></ul> |

## 错误码
| **error** | **errorMessage** | **描述** |
| --- | --- | --- |
| 3 | unknown error! | 未知错误 |
| 62003 | 系统出错，正在排查 | 系统出错，正在排查 |
