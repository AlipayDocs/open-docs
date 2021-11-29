
# 简介
不再信任该 SSID，对于需要 Portal 认证的 WIFI，继续弹出 portal 认证页面。为 **iOS特有接口**。

# 使用限制

- **基础库** [1.14.0](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js示例代码
```javascript
if (my.env.platform === 'iOS') {
  my.unregisterSSID({
    SSID: '',
    success: function(res) {
      console.log(res)
    }
  })
}
```

## 入参

Object 类型，属性如下：

| **名称** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| SSID | String | 是 | Wi-Fi 设备 SSID。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

