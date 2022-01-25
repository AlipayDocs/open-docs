
# 简介
**my.ap.navigateToAlipayPage** 是用于小程序中跳转到支付宝官方业务或运营活动页面的 API。

小程序之间相互跳转，请使用专有接口：[my.navigateToMiniProgram](https://opendocs.alipay.com/mini/api/yz6gnx)。

小程序各场景下的跳转限制及实现方法请见：[小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

1. 使用 appCode 属性：
```javascript
// .js
my.ap.navigateToAlipayPage({
    appCode:'tinyAppSHH',
    appParams: {},
    success:(res) => {
        my.alert({content:'成功：'+JSON.stringify(res)});
    },
    fail:(res) => {
        my.alert({content:'失败：'+JSON.stringify(res)});
    }
}); 
// 打开支付宝扫一扫
my.ap.navigateToAlipayPage({
    appCode:'alipayScan',
    success:(res) => {
        my.alert({content:'成功：'+JSON.stringify(res)});
    },
    fail:(res) => {
        my.alert({content:'失败：'+JSON.stringify(res)});
    }
});
// 打开蚂蚁森林
my.ap.navigateToAlipayPage({
    appCode:'antForest',
    appParams: {
        autoShowProps:1 //可选参数，等1时，默认打开开启森林背包
    },
  success:(res) => {
        my.alert({content:'成功：'+JSON.stringify(res)});
    },
    fail:(res) => {
        my.alert({content:'失败：'+JSON.stringify(res)});
    }
});
// 打开股票详情
my.ap.navigateToAlipayPage({
   'appCode':"stockDetail",
   'appParams':{
        'stockType':"ES", //股票类型，ES-个股，MRI-指数
        'market':"N", //所在市场，SH-沪市，SZ-深，A\O\N\USI - 美股市场，HK-港股市场
        'symbol':"BABA", //股票代码
        'name':"阿里巴巴" //股票名称
    },
    success:(res) => {
        my.alert({content:'成功：'+JSON.stringify(res)});
    },
    fail:(res) => {
        my.alert({content:'失败：'+JSON.stringify(res)});
    }
});
```

2. 使用 path 属性，通过 scheme 跳转：

   - scheme 可以理解为一种特殊的URI，格式与 URI 相同。
   - 在 scheme 中配置的启动参数需要与 appId 同级，如果启动参数的值包含特殊字符，必须注意需要经过 encode 后再传递。
   - **注意**：并不是所有 scheme 都支持跳转，不支持的会报错（[错误码 2](https://opendocs.alipay.com/mini/api/navigatetoalipaypage#%E9%94%99%E8%AF%AF%E7%A0%81)）。
```javascript
// .js
my.ap.navigateToAlipayPage({
    // 例如跳转到支付宝出行页面
    path: 'alipays://platformapi/startapp?appId=200011235',
    success: () => {
        my.alert({ content: '成功' });
    },
    fail: (error) => {
        my.alert({ content: '失败：' + JSON.stringify(error) });
    }
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| appCode | String | 是（和 path 二选一） | 要跳转的支付宝官方业务，例如付款码，appCode: 'payCode'，详见下方 **appCode 参数说明**。<li>跳转支付宝扫一扫、收到的红包页面、爱攒油页面、小程序快报生活号、蚂蚁森林、蚂蚁庄园、某只股票的详情页，请使用 appCode 属性。</li><li>支付宝客户端 10.1.62 版本开始支持。</li><li>个人小程序暂不支持跳转付款码页面。</li>|
| path | String | 是（和 appCode 二选一） | 跳转 appCode 涵盖范围之外的支付宝业务、运营活动页面，请使用 path 属性。可传入 scheme 或 URL：<li>scheme 以 alipays://platformapi/startapp? 开头。受内部白名单以及当前小程序权限控制，只有部分 scheme 是可跳转的。暂不公开提供可跳转的 scheme 列表和权限申请界面，具体可用的取值请参考相关业务文档或咨询技术支持。</li><li>URL 仅支持以 https://render.alipay.com/p/c/ 开头。如果 URL 中带有参数，请先将整个 URL 做 encode 处理。</li> |
| appParams | Object | 否 | appCode 配套参数，需要和 appCode 搭配使用。目前已开放的跳转页面，均无需配置 appParams 参数，appParams 为 {} 即可。（见示例代码 2）<br />支付宝客户端 10.1.62 版本开始支持。 |


### appCode 参数说明
入参为 Object 类型，属性如下：

| **appCode** | **appParams** | **描述** |
| --- | --- | --- |
| alipayScan | {} | 打开支付宝扫一扫。 |
| redPacket | {} | 打开收到的红包页面。 |
| collectOil | {} | 打开爱攒油页面。 |
| tinyAppSHH | {} | 打开小程序快报生活号。 |
| antForest | **autoShowProps**：是否打开背包，可空。 | 打开蚂蚁森林。 |
| antFarm | {} | 打开蚂蚁庄园。 |
| stockDetail | **stockType**：股票类型，ES-个股，MRI-指数；<br />**market**：所在市场，SH-沪市，SZ-深，A\O\N\USI - 美股市场，HK-港股市场；**symbol**：股票代码；**name**：股票名称，需要encode。 | 打开某只股票的详情页。 |
| payCode | {} | 打开支付宝付款码。<br />**注意**：个人小程序暂不支持跳转付款码页面。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | 跳转成功。 |


### fail 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误信息。 |


## 错误码
| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 2 | 参数错误，打开失败。 | <li>path 和 appCode 二选一，必填。</li><li>请检查 appCode 入参是否填写有误，或者检查 path 参数（scheme 或 URL）格式是否正确。</li><li>对于 path 传入 scheme 的情况，请注意并非所有 scheme 都可跳转，具体可用的取值请参考相关业务文档或联系技术支持；对于 path 传入 URL 的情况，请注意 URL 必须以 https://render.alipay.com/p/c/ 开头。</li> |


## 常见问题 FAQ

### Q1：使用 my.ap.navigateToAlipayPage 是否可以跳转基金页面？
A：my.ap.navigateToAlipayPage 暂不支持跳转基金页面。

### Q2：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何提示“参数错误，打开失败”？
A：URL 格式错误或超出允许范围。请参考上文 [错误码 2](https://opendocs.alipay.com/mini/api/navigatetoalipaypage#%E9%94%99%E8%AF%AF%E7%A0%81) 的解决方案。
在错误码 2 的情况下，客户端界面上也会有 toast 提示。当前 iOS 上提示文案为 **参数错误，打开失败**，Android 上为 **打开失败，无权限**，实质相同。

### Q3：使用 my.ap.navigateToAlipayPage 跳转生活号文章有一个过渡空白过程，是否正常？
A：是正常的，属于正常加载流程。

### Q4：香港支付宝小程序支持“跳转支付宝应用或页面”my.ap.navigateToAlipayPage 吗？
A：针对国际业务的特殊性，支付宝有专门的团队支持，香港版小程序咨询请点击以下链接进行咨询：[https://global.alipay.com/open/faq.htm](https://global.alipay.com/open/faq.htm) 。

## 相关文档

- [小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)
- [my.navigateToMiniProgram](https://opendocs.alipay.com/mini/api/yz6gnx)
