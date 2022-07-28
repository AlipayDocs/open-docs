# 简介
**my.ap.navigateToAlipayPage** 是用于跳转到支付宝官方业务或运营活动页面的 API。

在小程序中跳转支付宝业务或打开链接，请按下表分情况处理：
<table>
<tr>
  <td colspan=2>跳转目标</td>
  <td>跳转方法</td>
</tr>
<tr>
  <td rowspan=3>支付宝业务</td>
  <td>后文 <b>appCode 列表</b> 所列举的业务</td>
  <td>使用 my.ap.navigateToAlipayPage()</td>
</tr>
<tr>
  <td>已知 appId 的官方小程序</td>
  <td>使用 <a taget="_blank" href="https://opendocs.alipay.com/mini/api/yz6gnx">my.navigateToMiniProgram()</a></td>
</tr>
<tr>
  <td>其他情况</td>
  <td>联系合作的支付宝业务人员</td>
</tr>
<tr>
  <td rowspan=3>支付宝 URL<br><i>https&colon;//*.alipay.com/*</i></td>
  <td>以 https&colon;//render.alipay.com/p/ 开头的 URL</td>
  <td>使用 my.ap.navigateToAlipayPage()</td>
</tr>
<tr>
  <td>域名为 ur.alipay.com 或 m.alipay.com 的短链接<br>或以 https&colon;//ds.alipay.com/?scheme= 开头的 URL</td>
  <td>参考本文档 <b>附录 1</b>，先将 scheme 转换为实际目标地址</td>
</tr>
<tr>
  <td>其他情况</td>
  <td><b>申请添加白名单</b>，然后使用 my.ap.navigateToAlipayPage()</td>
</tr>
<tr>
  <td rowspan=3>支付宝 scheme<br><i>alipays://*</i></td>
  <td>scheme 中的 appId 为 16 位</td>
  <td><a taget="_blank" href="https://opendocs.alipay.com/mini/0090ty">转换成 my.navigateToMiniProgram() 调用</a></td>
</td>
<tr>
  <td>scheme 中的 appId 为 20000067</td>
  <td>参考本文档 <b>附录 1</b>，先将 scheme 转换为实际目标地址</td>
</td>
<tr>
  <td>其他情况</td>
  <td><b>申请添加白名单</b>，然后使用 my.ap.navigateToAlipayPage()</td>
</tr>
<tr>
  <td rowspan=2>非支付宝 URL</td>
  <td>开发者自有域名</td>
  <td>使用 <a taget="_blank" href="https://opendocs.alipay.com/mini/component/web-view">web-view 组件</a></td>
</tr>
<tr>
  <td>第三方域名</td>
  <td><b>申请添加白名单</b>，然后使用 my.ap.navigateToAlipayPage()</td>
</tr>
</table>

上表中需要 **申请添加白名单** 的情况，所涉及的 URL 或 scheme 均为支付宝业务人员出于特殊合作需要定向提供给小程序开发者，并通过内部流程添加白名单（否则无法跳转）。暂不提供申请添加白名单的线上流程，如有相关诉求，请联系合作的支付宝业务人员。

本文档的 <b>附录</b> 部分提供了链接转换和代码生成的示例。在对上表内容有了解的基础上，开发者可直接使用附录代码作为工具，取代人工判断。

关于小程序各场景下的跳转限制及实现方法，可查看 [小程序跳转 FAQ](https://opendocs.alipay.com/mini/0090ty)。


## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

1. 使用 appCode：
```javascript
// 打开支付宝扫一扫
my.ap.navigateToAlipayPage({
  appCode:'alipayScan',
  success:(res) => {
    console.log('navigateToAlipayPage success', JSON.stringify(res));
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
    console.log('navigateToAlipayPage success'，JSON.stringify(res));
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
    console.log('navigateToAlipayPage success',JSON.stringify(res));
  },
  fail:(res) => {
    my.alert({ title: 'navigateToAlipayPage fail', content: JSON.stringify(res) });
  }
});

// 跳转支付宝 scheme
my.ap.navigateToAlipayPage({
  path: 'alipays://platformapi/startapp?appId=00000000', // 注意 scheme 需要申请添加白名单
  success:(res) => {
    console.log('navigateToAlipayPage success'，JSON.stringify(res));
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
| 2 | 参数错误，打开失败。<br><br>注：旧版本（10.2.70 以下）客户端界面上也会有相应 toast 提示。 | <ul><li>如使用 appCode，请检查拼写是否有误。</li><li>如使用 path，请确保传入的参数是以 'https://render.alipay.com/p/' 开头或已由支付宝业务人员为当前小程序添加白名单。</li></ul> |

# 常见问题

## Q：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何提示“参数错误，打开失败”？
A：一般都是因为 URL 不是以 'https://render.alipay.com/p/' 开头且未添加白名单，跳转失败（进于 fail 回调），低版本客户端伴有 toast 提示。处理办法请参考本文档 **简介** 部分的指引表格及关于添加白名单的说明。

## Q：使用 my.ap.navigateToAlipayPage 打开 H5 页面为何发生 url 参数丢失？
A：历史原因，此接口要求对 url 做二次编码再传入，即需要向 path 传入 encodeURIComponent(url），否则内部的 decode 过程可能造成 url 的参数被破坏。

## Q：使用 my.ap.navigateToAlipayPage 跳转生活号文章有一个过渡空白过程，是否正常？
A：是正常的，属于生活号文章页本身特有的加载流程。

## Q：使用 my.ap.navigateToAlipayPage 是否可以跳转基金页面？
A：暂不支持跳转基金页面。

## Q：香港支付宝小程序支持 my.ap.navigateToAlipayPage 吗？
A：针对国际业务的特殊性，支付宝有专门的团队支持，关于香港版小程序的咨询请点击以下链接：[https://global.alipay.com/open/faq.htm](https://global.alipay.com/open/faq.htm) 。

# 附录

## 附录 1. 获取实际目标地址的代码
```javascript
/*
 * 以下代码主要用于演示如何将链接转换为实际目标地址（以便恰当地选择跳转方法/申请添加白名单），亦可用作开发辅助工具
 * 代码运行需要 Node.js 环境
 */

const https = require('https');
const http = require('http');

// 将跳转链接解析为实际目标地址
// 返回 Promise
//  - 解析成功：resolve({ result, trace })，result 为目标地址，trace 为中间结果
//  - 解析失败：resolve({ error, trace })，error 为错误信息，trace 为中间结果
function getRealTarget(url) {
  const getLocation = url => new Promise((resolve, reject) => {
    if (!/^https?:\/\/(ur|m)\.alipay\.com/i.test(url)) {
      return resolve(url);
    }
    const req = (url.startsWith('https:') ? https : http).request(url, {
      method: 'HEAD',
      timeout: 1000,
    }, res => {
      res.resume();
      const status = res.statusCode;
      if (status == 301 || status == 302) {
        resolve(res.headers.location);
      } else {
        resolve(url);
      }
    });
    req.setTimeout(500, () => req.abort());
    req.on('error', reject);
    req.end();
  });
  
  const getParams = url => {
    const params = {};
    for (let [ key, value ] of new URL(url).searchParams) {
      params[key] = value;
    }
    return params;
  };
  
  const onlyHasKeys = (obj, keys) => {
    const kset = new Set(keys);
    for (let key in obj) {
      if (!kset.has(key)) {
        return false;
      }
    }
    return true;
  };
  
  const trace = [];
  const fail = (msg, last) => {
    trace.push(last);
    return Promise.resolve({ error: msg, trace });
  };
  const success = () => {
    return Promise.resolve({ result: trace[trace.length - 1], trace });
  };
  
  const resolveUrl = url => {
    if (trace.indexOf(url) < 0) {
      trace.push(url);
    } else {
      return fail('redirect loop', url);
    }
    if (url.startsWith('https://ds.alipay.com/?scheme=') ||
      url.startsWith('https://render.alipay.com/p/s/i/?scheme=')) {
      const { scheme } = getParams(url);
      if (scheme.startsWith('alipays://')) {
        return resolveUrl(scheme);
      } else {
        return fail('no scheme in url', scheme);
      }
    }
    if (url.startsWith('https://m.alipay.com/') || url.startsWith('https://ur.alipay.com/')) {
      return getLocation(url).then(location => {
        return location == url ? success() : resolveUrl(location);
      });
    }
    if (url.startsWith('alipays://')) {
      const params = getParams(url);
      if (params.appId == '20000067' && onlyHasKeys(params, ['appId', 'url'])) {
        if (/^https?:\/\//.test(params.url)) {
          return resolveUrl(params.url);
        }
        return fail('no url in scheme', params.url);
      }
      if (/^\d{16}$/.test(params.appId) && onlyHasKeys(params, ['appId', 'page', 'query'])) {
        const { appId, page, query } = params;
        trace.push(JSON.parse(JSON.stringify({
          appId,
          path: page || void(0),
          query: query ? getParams('x:?' + query) : void(0)
        })));
        return success();
      }
    }
    return success();
  };
  
  return resolveUrl(url);
}

// 调用示例：解析 URL
getRealTarget('https://ur.alipay.com/1AjU8c').then(console.log);

// 调用示例：解析 scheme
getRealTarget('alipays://platformapi/startapp?appId=2021002143614743&page=pages/index/index').then(console.log);

```

## 附录 2. 生成跳转代码的代码
```javascript
/*
 * 以下代码主要用于演示如何针对跳转目标选择跳转方法，亦可用作开发辅助工具
 */

// 生成跳转代码
// 参数 target，接受附录 1 中的 getRealTarget(url) 得到的 result，两种形式：
//  - 字符串: url 或 scheme
//  - Object: { appId, path, query }
// 返回的代码中包含的错误处理，其中 console.log 打印的信息供开发者参考
function generateCode(target) {
  var prep, api, params, fail;
  if (typeof target == 'string') {
    prep = `var targetUrl = ${JSON.stringify(target)};\n`;
    api = 'my.ap.navigateToAlipayPage';
    params = { path: target.startsWith('alipays://') ? '${targetUrl}' : '${encodeTargetUrl}' };
    if (!target.startsWith('https://render.alipay.com/p/')) {
      params.fail = '${fail}';
    }
    fail = target.startsWith('alipays://') || /^https:\/\/[^\/]+\.alipay\.com\//.test(target) ? res => {
      console.log('navigateToAlipayPage 失败。目标地址', targetUrl, '未加白，请联系合作的支付宝业务人员');
      my.showToast({ content: '跳转失败' });
    } : res => {
      console.log('navigateToAlipayPage 失败。目标地址', targetUrl, '未加白，请考虑使用 web-view 组件或联系合作的支付宝业务人员');
      my.showToast({ content: '跳转失败' });
    };
  } else {
    if (!target.appId || target.appId.length != 16) {
      throw new Error('navigateToMiniProgram 只支持 16 位 appId');
    }
    prep = '';
    api = 'my.navigateToMiniProgram';
    params = { ...target, fail: '${fail}' };
    fail = res => {
      if (res.error == 30) {
        my.alert({ content: '目标小程序设置了不允许跳转' });
      } else {
        console.log('navigateToMiniProgram 失败，目标 appId 无效或网络暂不可用');
        my.showToast({ content: '跳转失败' });
      }
    };
  }
  return `${prep}${api}(${JSON.stringify(params, null, 2)});`
    .replace('"${targetUrl}"', 'targetUrl')
    .replace('"${encodeTargetUrl}"', 'encodeURIComponent(targetUrl)')
    .replace('"${fail}"', fail ? fail.toString().replace(/^  /mg, '') : '');
}

// 示例：跳转支付宝活动页
var code = generateCode('https://render.alipay.com/p/404');
console.log(code, '\n');

// 示例：跳转非支付宝页面
var code = generateCode('https://www.baidu.com/');
console.log(code, '\n');

// 示例：跳转支付宝 scheme
var code = generateCode('alipays://platformapi/startapp?appId=20000042');
console.log(code, '\n');

// 示例：跳转小程序
var code = generateCode({ appId: '2000000020000000', path: '/pages/index/index', query: { x: 100 } });
console.log(code, '\n');

```
