# 简介
**my.ap.navigateToAlipayPage** 是用于跳转到支付宝官方业务或运营活动页面的 API。

在小程序中跳转支付宝业务或打开链接，请按下表分情况处理：


上表中 **申请添加白名单** 的情况，所涉及的 URL 或 scheme 一般均为支付宝业务人员出于特殊合作需要定向提供给小程序开发者，并通过内部流程添加白名单（否则无法跳转）。暂不提供自助申请入口，如有相关诉求，请联系合作的支付宝业务人员。


关于小程序各场景下的跳转限制及实现方法，可查看 [小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)。


## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

1. 使用 appCode：
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

// 打开指定股票详情页
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

2. 使用 path
```javascript
// 打开支付宝运营活动页
my.ap.navigateToAlipayPage({
  path: encodeURIComponent('https://render.alipay.com/p/404'), // 注意只支持特定前缀的 URL，且需要整体冗余编码
  success:(res) => {
    console.log('navigateToAlipayPage success'，JSON.stringify(res)});
  },
  fail:(res) => {
    my.alert({ title: 'navigateToAlipayPage fail', content: JSON.stringify(res) });
  }
});

// 跳转支付宝 scheme
my.ap.navigateToAlipayPage({
  path: 'alipays://platformapi/startapp?appId=00000000', // 注意 scheme 需要申请添加白名单
  success:(res) => {
    console.log('navigateToAlipayPage success'，JSON.stringify(res)});
  },
  fail:(res) => {
    my.alert({ title: 'navigateToAlipayPage fail', content: JSON.stringify(res) });
  }
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| appCode | String | 是（与 path 二选一） | 跳转目标业务标识，与 path 二选一。完整列表见下文 **appCode 列表**。<br>支付宝客户端自 10.1.62 版本开始支持此参数。|
| appParams | Object | 否 | 与 appCode 配套使用的跳转参数。使用方法参考代码示例 1，字段名称和取值见下文 **appCode 列表**。 |
| path | String | 是（与 appCode 二选一） | 跳转目标链接地址，与 appCode 二选一。接受 encodeURIComponent(URL) 或 scheme。默认只支持以 `https://render.alipay.com/p/` 开头的支付宝页面 URL。跳转 scheme 或者不含指定前缀的 URL，均需支付宝业务人员为当前小程序添加白名单，请参考此文档 **简介** 部分。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### appCode 列表

| **appCode** | **appParams** | **跳转目标** |
| --- | --- | --- |
| alipayScan | 无 | 支付宝扫一扫 |
| redPacket | 无 | 收到的红包页面 |
| collectOil | 无 | 爱攒油页面 |
| tinyAppSHH | 无 | 小程序快报生活号 |
| antForest | <ul><li>**autoShowProps**：是否显示背包，取值 0 或者 1，默认为 0（不显示）</li></ul> | 蚂蚁森林 |
| antFarm | 无 | 蚂蚁庄园 |
| stockDetail | <ul><li>**symbol**：股票代码，如 'BABA'</li><li>**market**：股票所在市场，如 'N'。可用值 'SH' / 'SZ' / 'HK' / 'A' / 'O' / 'N' / 'USI'</li></ul> | 股票详情页 |
| payCode | 无 | 支付宝付款码 <br/>**注意**：个人小程序不支持跳转付款码。 |

## 错误码
fail 回调的参数为一个 Object，其 error 属性为错误码
| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 2 | 参数错误，打开失败。<br><br>注：旧版本（10.2.70 以下）客户端界面上也会有相应 toast 提示。 | <ul><li>如使用 appCode，请检查拼写是否有误。</li><li>如使用 path，请确保传入的参数是以 https://render.alipay.com/p/ 开头或已由支付宝业务人员为当前小程序添加白名单。</li></ul> |

# 常见问题

## Q：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何提示“参数错误，打开失败”？
A：一般都是因为 URL 不是以 https://render.alipay.com/p/ 开头且未添加白名单，导致不能跳转，低版本客户端伴有 toast 提示。处理办法请参考本文档**简介**部分的表格及说明。

## Q：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何发生 url 参数丢失？
A：历史原因，此接口要求对 url 做二次编码再传入，即需要向 path 传入 encodeURIComponent(url），否则内部的 decode 过程可能造成 url 的子参数丢失/混乱。

## Q：使用 my.ap.navigateToAlipayPage 跳转生活号文章有一个过渡空白过程，是否正常？
A：是正常的，属于正常加载流程。

## Q：使用 my.ap.navigateToAlipayPage 是否可以跳转基金页面？
A：暂不支持跳转基金页面。

## Q：香港支付宝小程序支持 my.ap.navigateToAlipayPage 吗？
A：针对国际业务的特殊性，支付宝有专门的团队支持，关于香港版小程的咨询请点击以下链接：[https://global.alipay.com/open/faq.htm](https://global.alipay.com/open/faq.htm) 。

# 相关文档

- [小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)
- [web-view H5 页面承载](https://opendocs.alipay.com/mini/component/web-view)
- [my.navigateToMiniProgram](https://opendocs.alipay.com/mini/api/yz6gnx)
