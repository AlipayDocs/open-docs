# 简介
**my.ap.navigateToAlipayPage** 是用于从小程序跳转到支付宝官方业务或运营活动页面的 API。

本接口支持三类参数：

1. 由 appCode 公开声明的支付宝客户端内业务。后文 **appCode列表** 有列举。


2. 支付宝运营活动页面 URL，以 https://render.alipay.com/p/ 开头。

* 注意：支付宝短链接（域名一般为 ur.alipay.com、m.alipay.com）URL 并不支持用此接口打开，如有在小程序里打开的必要，请使用后文 **常见问题 FAQ** 所提供的代码先进行解析和判断，以选择正确的打开方式。

* 注意：非支付宝官方的 URL，自有域名的请使用 [&lt;web-view&gt;](https://opendocs.alipay.com/mini/component/web-view) 
组件；第三方域名原则上不支持打开，如有特殊行业特殊需求，请联系所对接的支付宝 BD。

3. 支付宝客户端的 scheme。以 alipays://platformapi/startapp? 开头。这些 scheme 一般出于特殊的业务接入或合作需要，由支付宝 BD 提供给特定小程序并通过内部流程定向添加白名单。

* 注意：用于从外部 App（如手机浏览器）唤起支付宝并打开小程序的 scheme，并不支持在小程序内部作为参数传给 my.ap.navigateToAlipayPage，请转换成 [my.navigateToMiniProgram()](https://opendocs.alipay.com/mini/02sz8n#%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%20FAQ) 调用。


关于小程序各场景下的跳转限制及实现方法，可查看 [小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)。


## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

1. 跳转 appCode：
```javascript
// 打开支付宝扫一扫
my.ap.navigateToAlipayPage({
  appCode:'alipayScan',
  success:(res) => {
    console.log('navigateToAlipayPage success'，JSON.stringify(res)});
  },
  fail:(res) => {
    my.alert({ title: 'navigateToAlipayPage fail', content: JSON.stringify(res) });
  }
});
// 以指定参数打开股票详情页
my.ap.navigateToAlipayPage({
  appCode: 'stockDetail',
  appParams: {
    symbol: 'BABA',
    market: 'N',
  },
  success:(res) => {
    console.log('navigateToAlipayPage success'，JSON.stringify(res)});
  },
  fail:(res) => {
    my.alert({ title: 'navigateToAlipayPage fail', content: JSON.stringify(res) });
  }
});
```

2. 跳转支付宝 URL：<br>
注意：只支持打开 https://render.alipay.com/p/ 开头的 URL。
```javascript
my.ap.navigateToAlipayPage({
  path: 'https://render.alipay.com/p/404', // 404 页面
  success:(res) => {
    console.log('navigateToAlipayPage success'，JSON.stringify(res)});
  },
  fail:(res) => {
    my.alert({ title: 'navigateToAlipayPage fail', content: JSON.stringify(res) });
  }
})
```

3. 跳转支付宝 scheme：<br>
注意：只有极少数 scheme 是所有小程序都可跳转，大部分需要通过 BD 走特殊申请。
```javascript
my.ap.navigateToAlipayPage({
  path: 'alipays://platformapi/startapp?appId=200011235', // 支付宝出行
  success:(res) => {
    console.log('navigateToAlipayPage success'，JSON.stringify(res)});
  },
  fail:(res) => {
    my.alert({ title: 'navigateToAlipayPage fail', content: JSON.stringify(res) });
  }
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| appCode | String | 是（和 path 二选一） | 要跳转的支付宝官方业务，例如付款码 payCode。完整列表见下文 **appCode 列表**。|
| appParams | Object | 否 | appCode 配套参数，需要和 appCode 搭配使用。使用方法参考上文示例 1，具体取值请参考 **appCode 列表** |
| path | String | 是（和 appCode 二选一） | 跳转 appCode 涵盖范围之外的支付宝业务、运营活动页面，请使用 path 属性。可传入 scheme 或 URL：<ul><li>scheme 以 alipays://platformapi/startapp? 开头。scheme 的具体取值，请根据需要自行向合作的支付宝运营人员或 BD 索取。支付宝人员在给出 scheme 的同时，也会为申请方小程序添加入白单，否则无法跳转。</li><li>URL：仅支持以 https://render.alipay.com/p/ 开头的页面地址。如果目标页面 url 中包含参数，请向 path 传入 encodeURIComponent(url) </li></ul> |


### appCode 列表

| **appCode** | **描述** | **appParams 字段** |
| --- | --- | --- |
| alipayScan | 支付宝扫一扫 | - |
| redPacket | 收到的红包页面 | - |
| collectOil | 爱攒油页面 | - |
| tinyAppSHH | 小程序快报生活号 | - |
| antForest | 蚂蚁森林 | <ul><li>**autoShowProps**：是否显示背包</li></ul> |
| antFarm | 蚂蚁庄园 | - |
| stockDetail | 股票 | <ul><li>**stockType**：股票类型，ES-个股，MRI-指数</li><li>**market**：所在市场，SH-沪市，SZ-深，A\O\N\USI - 美股市场，HK-港股市场</li><li>**symbol**：股票代码</li><li>**name**：股票名称，需要 encode</li></ul> |
| payCode | 支付宝付款码 <br/>**注意**：个人小程序不支持跳转付款码。 | - |

### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | 跳转成功。 |

### Function fail
fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误信息。 |

## 错误码
| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 2 | 参数错误，打开失败。 | <ul><li>path 和 appCode 二选一，必填。</li><li>请检查 appCode 入参是否填写有误，或者检查 path 参数（scheme 或 URL）格式是否正确。</li><li>对于 path 传入 scheme 的情况，请注意并非所有 scheme 都可跳转，具体可用的取值请参考相关业务文档或联系技术支持；对于 path 传入 URL 的情况，请注意 URL 必须以 https://render.alipay.com/p/ 开头。</li></ul> |

# 常见问题

## Q1：使用 my.ap.navigateToAlipayPage 是否可以跳转基金页面？
A：my.ap.navigateToAlipayPage 暂不支持跳转基金页面。

## Q2：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何提示“参数错误，打开失败”？
A：URL 格式错误或超出允许范围。请参考上文 [错误码 2](https://opendocs.alipay.com/mini/api/navigatetoalipaypage#%E9%94%99%E8%AF%AF%E7%A0%81) 的解决方案。
在错误码 2 的情况下，客户端界面上也会有 toast 提示。当前 iOS 上提示文案为 **参数错误，打开失败**，Android 上为 **打开失败，无权限**，实质相同。

## Q3：使用 my.ap.navigateToAlipayPage 跳转生活号文章有一个过渡空白过程，是否正常？
A：是正常的，属于正常加载流程。

## Q4：香港支付宝小程序支持“跳转支付宝应用或页面”my.ap.navigateToAlipayPage 吗？
A：针对国际业务的特殊性，支付宝有专门的团队支持，香港版小程序咨询请点击以下链接进行咨询：[https://global.alipay.com/open/faq.htm](https://global.alipay.com/open/faq.htm) 。

# 相关文档

- [小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)
- [my.navigateToMiniProgram](https://opendocs.alipay.com/mini/api/yz6gnx)
