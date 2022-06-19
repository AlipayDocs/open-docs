# 简介
**my.ap.navigateToAlipayPage** 是用于从小程序跳转到支付宝官方业务或运营活动页面的 API。

在小程序中跳转官方业务或打开链接，请按下表分情况处理：



上表中 **申请添加白名单** 的情况，所涉及的 URL 或 scheme 一般均为支付宝业务人员出于特殊的业务接入或合作需要定向提供给小程序开发者，并通过内部流程添加白名单，暂不提供自助申请入口。如有相关诉求，请联系合作的支付宝业务人员。


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

2. 跳转支付宝运营活动页面：
```javascript
my.ap.navigateToAlipayPage({
  path: encodeURIComponent('https://render.alipay.com/p/404'), // 404 页面。注意只支持特定前缀的 URL，且需要整体 encode
  success:(res) => {
    console.log('navigateToAlipayPage success'，JSON.stringify(res)});
  },
  fail:(res) => {
    my.alert({ title: 'navigateToAlipayPage fail', content: JSON.stringify(res) });
  }
})
```

3. 跳转支付宝 scheme：
```javascript
my.ap.navigateToAlipayPage({
  path: 'alipays://platformapi/startapp?appId=200011235', // 支付宝出行。注意并非所有 scheme 都可直接使用
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
| appCode | String | 是（与 path 二选一） | 跳转目标业务标识，与 path 二选一。完整列表见下文 **appCode 列表**。|
| appParams | Object | 否 | 与 appCode 配套使用的跳转参数。使用方法参考代码示例 1，字段名称和取值见下文 **appCode 列表** |
| path | String | 是（与 appCode 二选一） | 跳转目标链接地址，与 appCode 二选一。接受 encodeURIComponent(URL) 或 scheme。默认只支持以 `https://render.alipay.com/p/` 开头的支付宝页面 URL。跳转 scheme 或者非指定前缀的 URL，均需支付宝业务人员为小程序定向添加白名单（否则报错，错误码 2），参考此文档 **简介** 部分。 |


### appCode 列表

| **appCode** | **描述** | **appParams 字段** |
| --- | --- | --- |
| alipayScan | 支付宝扫一扫 | - |
| redPacket | 收到的红包页面 | - |
| collectOil | 爱攒油页面 | - |
| tinyAppSHH | 小程序快报生活号 | - |
| antForest | 蚂蚁森林 | <ul><li>**autoShowProps**：是否显示背包，取值 0 或者 1，默认为 0（不显示）</li></ul> |
| antFarm | 蚂蚁庄园 | - |
| stockDetail | 股票详情 | <ul><li>**symbol**：股票代码，如 'BABA'</li><li>**market**：所在市场，取值 'SH'（沪市）/'SZ'（深）/'HK'（港股）/'A'/'O'/'N'/'USI'（美股）</li></ul> |
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
| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 2 | 参数错误，打开失败。<br>旧版本（10.2.70 以下）客户端界面上也会有 toast 提示“无权限”。 | <ul><li>如使用 appCode，请检查拼写是否有误。</li><li>如使用 path，请参考入参描述，确保传入的是以指定前缀开头的 URL，或者已由支付宝业务人员为当前小程序定向加白。</li><li></li></ul> |

# 常见问题

## Q：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何提示“参数错误，打开失败”？
A：一般都是因为 URL 未加入白名单。请参考本文档**简介**部分关于申请添加白名单的描述。

## Q：使用 my.ap.navigateToAlipayPage 跳转生活号文章有一个过渡空白过程，是否正常？
A：是正常的，属于正常加载流程。

## Q：使用 my.ap.navigateToAlipayPage 是否可以跳转基金页面？
A：my.ap.navigateToAlipayPage 暂不支持跳转基金页面。

## Q：香港支付宝小程序支持“跳转支付宝应用或页面”my.ap.navigateToAlipayPage 吗？
A：针对国际业务的特殊性，支付宝有专门的团队支持，香港版小程序咨询请点击以下链接进行咨询：[https://global.alipay.com/open/faq.htm](https://global.alipay.com/open/faq.htm) 。

# 相关文档

- [小程序跳转 FAQ](https://opendocs.alipay.com/mini/api/xqvxl4)
- [my.navigateToMiniProgram](https://opendocs.alipay.com/mini/api/yz6gnx)
