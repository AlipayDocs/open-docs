
# 简介
获取本次小程序启动时的参数。如果当前是冷启动，则返回值与 App.onLaunch 的回调参数一致；如果当前是热启动，则返回值与 App.onShow 一致。

## 使用限制

- 基础库 [2.7.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const options = my.getEnterOptionsSync();
console.log(options);
```

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| query | Object | 当前小程序的 query，从启动参数的 query 字段解析而来。<br />注意：若没有启动参数，则不会返回 query 参数。 |
| scene | String | 启动小程序的 [场景值](https://opendocs.alipay.com/mini/framework/scene)。 |
| path | String | 当前小程序的页面地址，从启动参数 page 字段解析而来，page 忽略时默认为首页。 |
| referrerInfo | Object | 来源消息。 |


### referrerInfo 子属性
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| appId | String | 来源小程序。 |
| extraData | Object | 来源小程序传过来的数据。 |

