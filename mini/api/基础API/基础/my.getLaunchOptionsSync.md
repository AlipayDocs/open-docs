# 简介

**my.getLaunchOptionsSync** 是获取小程序启动时的参数的 API。与 [App.onLaunch](<https://opendocs.alipay.com/mini/framework/app-detail#onLaunch(object%3A%20Object)%20%E5%8F%8A%20onShow(object%3A%20Object)>) 的回调参数一致。

该函数是获取 [冷启动](https://opendocs.alipay.com/mini/framework/operating-mechanism) 时的启动参数。针对 [热启动场景](https://opendocs.alipay.com/mini/framework/operating-mechanism)，可以使用 [my.getEnterOptionsSync](https://opendocs.alipay.com/mini/api/029i75)，该方法会获取最新进入小程序的参数。获取小程序启动时的参数的其他方法请参考：[如何在小程序启动后获取启动参数](https://opendocs.alipay.com/support/01rb2a)。

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
console.log(options);
```

## 返回值

返回一个 Object 类型的对象，其属性如下： | **属性** | **类型** | **描述** | | --- | --- | --- | | query | Object | 当前小程序的 query，从启动参数的 query 字段解析而来。<br />**注意**：若没有启动参数，则不会返回 query 参数。 | | scene | String | 启动小程序的 [场景值](https://opendocs.alipay.com/mini/framework/scene)。 | | path | String | 当前小程序的页面地址，从启动参数 page 字段解析而来，page 忽略时默认为首页。 | | referrerInfo | Object | 来源消息。 |

### Object referrerInfo

| **属性**  | **类型** | **描述**                 |
| --------- | -------- | ------------------------ |
| appId     | String   | 来源小程序。             |
| extraData | Object   | 来源小程序传过来的数据。 |

# 常见问题

## 小程序未上线，如何测试启动参数？

小程序未上架过版本，可通过开发版/体验版进行测试，详情参考【[调试跳转未上线小程序版本（开发版/体验版）](https://opendocs.alipay.com/support/01rb0j)】。

## 在 IDE 上如何测试启动参数？

请参考：[IDE 配置/获取全局参数和页面参数（启动参数）](https://opendocs.alipay.com/support/01rb7b)

## 如何从浏览器或外部 APP 携带参数跳转到小程序？

该 API 用来获取小程序启动参数。如果想从外部唤起小程序，可以通过唤起支付宝的 scheme 来跳转到小程序，在 scheme 中可以加入需要跳转的小程序、小程序页面、参数等。详情请参考：[小程序 scheme 链接介绍](https://opendocs.alipay.com/support/01rb18)。

社区有一篇较详细的讲解了小程序码或链接唤起的小程序如何获取启动参数的文档：[【经验分享】支付宝小程序如何获取外部链接携带的参数](https://forum.alipay.com/mini-app/post/35101021)。
