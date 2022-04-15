
# 简介
**my.getLaunchOptionsSync** 是获取小程序启动时的参数的 API。与 [App.onLaunch](https://opendocs.alipay.com/mini/framework/app-detail#onLaunch(object%3A%20Object)%20%E5%8F%8A%20onShow(object%3A%20Object)) 的回调参数一致。

## 使用限制
- 基础库 [1.21.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.75 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 部分版本在无 `referrerInfo` 的时候会返回 `undefined`，建议使用 `options.referrerInfo && options.referrerInfo.appId` 进行判断。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用
## 示例代码
### .js 示例代码
```javascript
// .js
let options = my.getLaunchOptionsSync();
console.log(options)
```

## 返回值
返回一个 Object 类型的对象，其属性如下：
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| query | Object | 当前小程序的 query，从启动参数的 query 字段解析而来。<br />**注意**：若没有启动参数，则不会返回 query 参数。 |
| scene | String | 启动小程序的 [场景值](https://opendocs.alipay.com/mini/framework/scene)。 |
| path | String | 当前小程序的页面地址，从启动参数 page 字段解析而来，page 忽略时默认为首页。 |
| referrerInfo | Object | 来源消息。 |

### Object referrerInfo
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| appId | String | 来源小程序。 |
| extraData | Object | 来源小程序传过来的数据。 |
