# 简介

my.ap.openAlipayApp 打开支付宝客户端内指定的应用。

此 API 能打开的应用限于官方公开的 **appCode 列表**（见后文说明）。没有 appCode 的情况下：
- 如果已知目标小程序的 appId（16 位数字），请使用 [my.navigateToMiniProgram](https://opendocs.alipay.com/mini/api/yz6gnx)。
- 如果已知目标页面链接，请使用 [my.ap.openURL](https://opendocs.alipay.com/mini/04iy2y)（**推荐先用[跳转辅助工具](https://apitools.alipay.com/tools/open-url)检测和生成代码**）。


## 使用限制

- 基础库 [2.7.20](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本，支付宝客户端 10.1.62 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 打开支付宝扫一扫
my.ap.openAlipayApp({
  appCode: 'alipayScan',
  fail: res => {
    my.alert({
      title: 'openAlipayApp fail',
      content: JSON.stringify(res),
    });
  },
});

// 打开指定股票详情页
my.ap.openAlipayApp({
  appCode: 'stockDetail',
  appParams: { symbol: 'BABA', market: 'N' },
  fail: res => {
    my.alert({
      title: 'openAlipayApp fail',
      content: JSON.stringify(res),
    });
  },
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| appCode | String | 是 | 目标业务标识。完整列表可查看 <a href='#appCode 列表'>appCode 列表</a>。 |
| appParams | Object | 否 | 跳转的附加参数，不同 appCode 参数不同，详情可查看 <a href='#appCode 列表'>appCode 列表</a>。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### appCode 列表
| **appCode** | **appParams** | **跳转目标** |
| --- | --- | --- |
| alipayScan | 无 | 支付宝扫一扫。 |
| redPacket | 无 | 收到的红包页面。 |
| collectOil | 无 | 爱攒油页面。 |
| tinyAppSHH | 无 | 小程序快报生活号。 |
| antForest | autoShowProps：是否显示背包。可选值：<ul><li>1：显示背包。</li><li>0：不显示背包。</li></ul>默认为 0。 | 蚂蚁森林。 |
| antFarm | 无 | 蚂蚁庄园。 |
| stockDetail | <ul><li>symbol：股票代码，例如 'BABA'。</li><li>market：股票所在市场，例如 'SH'。可选值：</li><ul><li>SH：上海股市。</li><li>SZ：深圳股市。</li><li>HK：香港股市。</li><li>A：A 股市场。</li><li>O：美国股市。</li><li>N：美国股市。</li><li>USI：美国股市。</li></ul></ul> | 股票详情页。 |
| payCode | 无 | 支付宝付款码。<br />**注意**：个人小程序不支持跳转付款码。 |

### Function fail

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误描述。 |

## 错误码
fail 回调的参数为 Object，其 error 属性为错误码，errorMessage 为错误消息。

| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 2 | 参数无效 | appCode 参数无效，请检查。 |
