# 简介

**my.ap.navigateToAlipayPage** 是用于跳转到支付宝官方业务或运营活动页面的 API。

**此 API 已停止维护，文档即将下线（线上已有业务不受影响）**。替代方案：
- 已知目标业务的 appCode，请使用 [my.ap.openAlipayApp](https://opendocs.alipay.com/mini/04p771) 跳转。
- 已知目标页面的 URL 或 scheme，请尝试使用 [my.ap.openURL](https://opendocs.alipay.com/mini/04iy2y) 。**推荐优先使用[跳转辅助工具](https://apitools.alipay.com/tools/open-url)检测和生成代码**。

## 跳转支付宝应用或页面指南

在小程序中跳转支付宝业务或打开链接，按下表分情况处理：

<table>
<tr>
  <td colspan=2>跳转目标</td>
  <td>跳转方法</td>
</tr>
<tr>
  <td rowspan=3>支付宝业务</td>
  <td>后文 <b>appCode 列表</b> 所列举的业务</td>
  <td>使用 my.ap.openAlipayApp()</td>
</tr>
<tr>
  <td>已知 appId 的官方小程序</td>
  <td>使用 <a taget="_blank" href="https://opendocs.alipay.com/mini/api/yz6gnx">my.navigateToMiniProgram()</a></td>
</tr>
<tr>
  <td>其他情况</td>
  <td>不支持跳转</td>
</tr>
<tr>
  <td rowspan=3>支付宝 URL<br><i>https&colon;//*.alipay.com/*</i></td>
  <td>以 https&colon;//render.alipay.com/p/ 开头的 URL</td>
  <td>使用 my.ap.openURL()</td>
</tr>
<tr>
  <td>域名为 ur.alipay.com 或 m.alipay.com 的短链接<br>或以 https&colon;//ds.alipay.com/?scheme= 开头的 URL</td>
  <td>使用 <a taget="_blank" href="https://apitools.alipay.com/tools/open-url">跳转辅助工具</a>检测并生成代码</td>
</tr>
<tr>
  <td>其他情况</td>
  <td><a taget="_blank" href="https://opendocs.alipay.com/mini/04iy2y#%E5%BC%80%E6%94%BE%E8%8C%83%E5%9B%B4">开放范围</a>内的小程序，使用 my.ap.openURL（需在小程序控制台申请添加白名单）；其他类目的小程序，暂不支持跳转</td>
</tr>
<tr>
  <td rowspan=3>支付宝 scheme<br><i>alipays://*</i></td>
  <td>scheme 中的 appId 为 16 位</td>
  <td><a taget="_blank" href="https://opendocs.alipay.com/mini/0090ty">转换成 my.navigateToMiniProgram() 调用</a></td>
</td>
<tr>
  <td>scheme 中的 appId 为 20000067</td>
  <td>使用 <a taget="_blank" href="https://apitools.alipay.com/tools/open-url">跳转辅助工具</a>检测并生成代码</td>
</td>
<tr>
  <td>其他情况</td>
  <td><a taget="_blank" href="https://opendocs.alipay.com/mini/04iy2y#%E5%BC%80%E6%94%BE%E8%8C%83%E5%9B%B4">开放范围</a>内的小程序，使用 my.ap.openURL（需在小程序控制台申请添加白名单）；其他类目的小程序，暂不支持跳转</td>
</tr>
<tr>
  <td rowspan=2>非支付宝 URL</td>
  <td>开发者自有页面</td>
  <td>使用 <a taget="_blank" href="https://opendocs.alipay.com/mini/component/web-view">web-view 组件</a><br>需要在小程序后台添加域名并上传校验文件</td>
</tr>
<tr>
  <td>第三方页面</td>
  <td><a taget="_blank" href="https://opendocs.alipay.com/mini/04iy2y#%E5%BC%80%E6%94%BE%E8%8C%83%E5%9B%B4">开放范围</a>内的小程序，使用 my.ap.openURL（需在小程序控制台申请添加白名单）；其他类目的小程序，暂不支持跳转</td>
</tr>
</table>

注：上表中链接类目标的跳转逻辑，均已集成到 **[跳转辅助工具](https://apitools.alipay.com/tools/open-url)**，推荐使用它来做检测并生成代码。


## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

1. 使用 appCode：

```javascript
// 打开支付宝扫一扫
my.ap.navigateToAlipayPage({
  appCode: 'alipayScan',
  success: res => {
    console.log('navigateToAlipayPage success', JSON.stringify(res));
  },
  fail: res => {
    my.alert({
      title: 'navigateToAlipayPage fail',
      content: JSON.stringify(res),
    });
  },
});

// 打开指定股票详情页
my.ap.navigateToAlipayPage({
  appCode: 'stockDetail',
  appParams: {
    symbol: 'BABA',
    market: 'N',
  },
  success: res => {
    console.log('navigateToAlipayPage success', JSON.stringify(res));
  },
  fail: res => {
    my.alert({
      title: 'navigateToAlipayPage fail',
      content: JSON.stringify(res),
    });
  },
});
```

2. 使用 path

```javascript
// 打开支付宝运营活动页
my.ap.navigateToAlipayPage({
  path: encodeURIComponent('https://render.alipay.com/p/404'), // 注意只支持特定前缀的 URL，且需要整体编码以后再传入
  success: res => {
    console.log('navigateToAlipayPage success', JSON.stringify(res));
  },
  fail: res => {
    my.alert({
      title: 'navigateToAlipayPage fail',
      content: JSON.stringify(res),
    });
  },
});

```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| appCode | String | 是（与 path 二选一） | 跳转目标业务标识，与 path 二选一。完整列表见下文 **appCode 列表**。<br>支付宝客户端自 10.1.62 版本开始支持此参数。 |
| appParams | Object | 否 | 与 appCode 配套使用的跳转参数。使用方法参考代码示例 1，字段名称和取值见下文 **appCode 列表**。 |
| path | String | 是（与 appCode 二选一） | 跳转目标页面地址，与 appCode 二选一。请传入 encodeURIComponent(url)，其中 url 为支付宝页面，必须以 `https://render.alipay.com/p/` 开头。 |
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
| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 2 | 跳转失败 (iOS） / 指定参数不可跳转，请检查或申请权限（Android） | <ul><li>如使用 appCode，请检查拼写是否有误。</li><li>如使用 path，请确保传入的参数为 encodeURIComponent('https://render.alipay.com/p/*')。 </li></ul> |
| 60001 | 处理异常，请稍后再试。 | API 内部异常，请稍后重试。 |

# 常见问题

## Q：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何提示“参数错误，打开失败”？

A：一般都是因为目标链接不在允许范围内（不是以 'https://render.alipay.com/p/' 开头）导致跳转失败（进于 fail 回调），低版本客户端伴有 toast 提示。

## Q：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何发生 url 参数丢失？

A：历史原因，此接口要求对 url 整体编码再传入，即需要向 path 传入 encodeURIComponent(url），否则内部的 decode 过程可能造成 url 的参数被破坏。

## Q：使用 my.ap.navigateToAlipayPage 跳转生活号文章有一个过渡空白过程，是否正常？

A：是正常的，属于生活号文章页本身特有的加载流程。

## Q：使用 my.ap.navigateToAlipayPage 是否可以跳转基金页面？

A：暂不支持跳转基金页面。

关于各场景下小程序跳转的实现方法及限制的更多信息，可查阅 [小程序跳转 FAQ](https://opendocs.alipay.com/mini/0090ty)。
