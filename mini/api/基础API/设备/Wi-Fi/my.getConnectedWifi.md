
# 简介
获取已连接中的 Wi-Fi 信息。

# 使用限制

- **基础库** [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
my.getConnectedWifi({
  success: function(res) {
    console.log(res)
  }
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Funciton | 否 | 调用结束的回调函数（调用成功、失败都会执行。 |

<a name="98dc6c80-1"></a>
### success 返回值
| **属性** | **类型** | **秒速** |
| --- | --- | --- |
| wifi | WifiInfo | Wi-Fi 信息。 |

<a name="wifi-1"></a>
#### WifiInfo
| **属性** | **类型** | **秒速** |
| --- | --- | --- |
| SSID | String | Wi-Fi 的 SSID。 |
| BSSID | String | Wi-Fi 的 BSSID。 |
| secure | Boolean | Wi-Fi 是否安全。 |
| signalStrength | Number | Wi-Fi 信号强度。取值 0 ～ 100，值越大强度越大。 |

