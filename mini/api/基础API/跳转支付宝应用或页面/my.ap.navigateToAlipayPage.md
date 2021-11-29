
# 简介
**my.ap.navigateToAlipayPage** 是用于小程序中跳转到支付宝官方业务或运营活动页面的 API。

小程序之间相互跳转，请使用专有接口：[my.navigateToMiniProgram](/mini/api/yz6gnx)。

小程序各场景下的跳转限制及实现方法请见：[小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
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
```javascript
// .js
my.ap.navigateToAlipayPage({
    // 例如跳转到共享单车页面，其 scheme 格式为：
    // alipays://platformapi/startapp?appId=60000155&chInfo=ch_${appid}，${appid} 替换为自己的16位 appid，例如：
    path:'alipays://platformapi/startapp?appId=60000155&chInfo=ch_${appid}',
    success:(res) => {
        my.alert({content:'系统信息' + JSON.stringify(res)});
    },
    fail:(error) => {
        my.alert({content:'系统信息' + JSON.stringify(error)});        
    }
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| appCode | String | 是（和 path 二选一） | 要跳转的支付宝官方业务，例如付款码，appCode: 'payCode'，详见下方 **appCode 参数说明**。<li>跳转支付宝扫一扫、收到的红包页面、爱攒油页面、小程序快报生活号、蚂蚁森林、蚂蚁庄园、某只股票的详情页，请使用 appCode 属性。</li><li>支付宝客户端 10.1.62 版本开始支持。</li><li>个人小程序暂不支持跳转付款码页面。</li>|
| path | String | 是（和appCode 二选一） | 要跳转的支付宝业务、运营活动 scheme 或 url，如果 url 中带有参数，请务必先将整个 url 做 encode 处理。<li>跳转除 appCode 参数涵盖的页面，请使用 path 属性。</li><li>可跳转域名以  alipays://platformapi/startapp ?开头的支付宝业务、运营页面。</li>|
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
| 2 | 参数错误，打开失败。 | <li>检查 H5 页面链接地址 scheme 或 URL 是否有误。</li><li>检查 appCode 入参是否有空格、是否填写有误。</li><li>path 和 appCode 二选一，必填。</li><li>可跳转域名以 [https://render.alipay.com/p/c]() 开头的支付宝业务、运营页面（生活号文章链接等）。部分支付宝运营、业务页面目前暂不开放跳转。</li>|
| 4 | 无权限调（N22104）。 | 个人小程序应用没有开放 my.ap.navigateToAlipayPage 能力。 |


## 常见问题 FAQ

### Q1：使用 my.ap.navigateToAlipayPage 是否可以跳转基金页面？
A：my.ap.navigateToAlipayPage 暂不支持跳转基金页面。

### Q2：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何提示“参数错误，打开失败”？
| **可能原因** | **解决方案** |
| --- | --- |
| H5 页面链接地址有误。 | 修改错误 H5 页面链接。 |
| 部分支付宝运营、业务页面目前暂不开放跳转。 | - |


### Q3：使用 my.ap.navigateToAlipayPage 跳转生活号文章有一个过渡空白过程，是否正常？
A：是正常的，属于正常加载流程。

### Q4：香港支付宝小程序支持"跳转支付宝应用或页面 " my.ap.navigateToAlipayPage 吗？
A：针对国际业务的特殊性，支付宝有专门的团队支持，香港版小程序咨询请点击以下链接进行咨询：[https://global.alipay.com/open/faq.htm](https://global.alipay.com/open/faq.htm) 。

## 相关文档

- [小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)
- [my.navigateToMiniProgram](https://opendocs.alipay.com/mini/api/yz6gnx)
