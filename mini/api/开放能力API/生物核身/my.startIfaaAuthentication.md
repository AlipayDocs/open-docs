# 简介
开始 IFAA 生物认证。

## 使用限制

- 基础库 [2.8.1](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.3.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
if (my.canIUse('startIfaaAuthentication')) {
    my.startIfaaAuthentication({
      requestAuthModes: ['fingerPrint'],
      challenge: 'my-test-challenge',
      success(res) {
        console.log(res.verifyId);
      },
      fail(res) {
        // 认证失败
        console.error(res);
      }
    })
  }
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| requestAuthModes | Array\<String\> | 是 | 请求使用的可接受的生物认证方式。可选值：<ul><li>fingerPrint：指纹识别。</li><li>facial：人脸识别。</li></ul> |
| challenge | String | 是 | 挑战因子。挑战因子为调用者为此次核身准备的关键识别信息，供调用者识别本次请求。例如：如果场景为请求用户对某订单进行授权确认，则可以将订单号填入此参数 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |

### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **说明** |
| --- | --- | --- |
| verifyId | String | 核身校验唯一标识，业务服务端二次校验时对应的入参 verify_id。 |

## 错误码
| **error** | **errorMessage** |
| --- | --- |
| 61001 | 校验失败 |
| 61003 | 用户取消 |
| 61004 | 任务超时 |
| 62002 | 未知异常 |
| 62003 | 网络异常 |
