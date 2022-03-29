# 简介
**my.request** 是用于发起网络请求的 API。

更多问题请参见 [my.request 常见问题](https://opendocs.alipay.com/mini/00hxw8)。

## 使用限制

- my.request 目前支持 GET/POST/PUT/DELETE（其中 PUT 和 DELETE 请求在支付宝客户端 10.1.95 或更高版本支持）。
- my.request 目前只支持 HTTPS 协议的请求。
- **基础库** [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；**支付宝客户端** 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
> 请预先在 [**支付宝小程序管理中心**](https://open.alipay.com/mini/dev/list) **> 小程序详情 > 设置 > 开发设置 > 服务器域名白名单** 中配置域名白名单。小程序在以下 API 调用时只能与白名单中的域名进行通讯：HTTP 请求（my.request）、上传文件（my.uploadFile）。
>
> ![|706x73](https://mdn.alipayobjects.com/afts/img/A*xM4NR6VRbfwccJpPkvUyrwBkAa8wAA/original?bz=openpt_doc&t=up10AFIkdB4BgOJNk-44NgAAAABkMK8AAAAA#align=left&display=inline&height=168&margin=%5Bobject%20Object%5D&originHeight=168&originWidth=1624&status=done&style=none&width=1624)
>
> **注意**：域名添加或删除后仅对新版本生效，老版本仍使用修改前的域名配置。
>
> 在 IDE 上进行调试时，请使用真机预览调试。
>
> 支付宝客户端已不再维护 [my.httpRequest](https://opendocs.alipay.com/support/01rb31#my.request%20%E4%B8%8E%20my.httpRequest%20%E7%9A%84%E5%8C%BA%E5%88%AB%E6%98%AF%E4%BB%80%E4%B9%88%EF%BC%9F)，建议使用 my.request。另外，钉钉客户端尚不支持 my.request。若在钉钉客户端开发小程序，则需要使用 my.httpRequest。

## 扫码体验
![|175x216](https://gw.alipayobjects.com/zos/skylark-tools/public/files/cedb01a73389c4346ed7c8c72de928a0.jpeg#align=left&display=inline&height=216&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=175)

**重要：**

- 小程序开发过程中，可在开发工具内 **详情 > 域名信息 > 忽略 http 请求域名合法性检查** 中选择是否忽略域名合法性检查，如果选择忽略，则在模拟器、预览以及真机调试场景不会校验域名合法性，但小程序上线前必须确保通讯域名在白名单内，否则在正式版本无法调用。
- my.request 的请求头默认值为 {'content-type': 'application/json'}，而不是 {'content-type': 'application/x-www-form-urlencoded'}。此外，请求头对象里面的 key 和 value 必须是 String 类型。

# 接口调用

## 示例代码
**注意**：案例仅供参考，建议使用自己的地址进行测试。

### dataType 为 json 示例
```javascript
// .js
my.request({
  url: 'https://httpbin.org/post',
  method: 'POST',
  data: {
    from: '支付宝',
    production: 'AlipayJSAPI',
  },
  headers:{
    'content-type':'application/json'  //默认值
  },
  dataType: 'json',
  success: function(res) {
    my.alert({content: 'success'});
  },
  fail: function(res) {
    my.alert({content: 'fail'});
  },
  complete: function(res) {
    my.hideLoading();
    my.alert({content: 'complete'});
  }
});
```

### dataType 为 Base64 示例
```javascript
// .js
my.request({
  url: 'https://gw.alipayobjects.com/mdn/miniapp_de/afts/img/A*G1kWSJbe2zEAAAAAAAAAAABjARQnAQ',
  method: 'GET',
  dataType: 'base64',
  success: (resp) => {
    console.log('resp data length', resp.data.length);
    console.log('resp data', resp.data); // 返回格式类似于：data:image/png;base64,iVBORw0KG...
  },
  fail: (err) => {
    console.log('error', err);
  },
});
```

### 调用 PUT 方法示例
**注意**：该方法在支付宝客户端 10.1.95 或更高版本开始支持。
```javascript
// .js
my.request({
  url: 'https://httpbin.org/put',
  method: 'PUT',
  data: {
    from: '支付宝',
    production: 'AlipayJSAPI',
  },
  headers:{
    'content-type':'application/json'  //默认值
  },
  dataType: 'json',
  success: function(res) {
    my.alert({content: 'success'});
  },
  fail: function(res) {
    my.alert({content: 'fail'});
  },
  complete: function(res) {
    my.hideLoading();
    my.alert({content: 'complete'});
  }
});
```

### 调用 DELETE 方法示例
**注意**：该方法在支付宝客户端 10.1.95 或更高版本开始支持。
```javascript
// .js
my.request({
      url: 'https://lb-bp1ex83f422co.sec.cloud.alipay.com/delete',
      method: 'DELETE',
      data: {
        from: '支付宝',
        production: 'AlipayJSAPI',
      },
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded'
      },
      dataType: 'json',
      responseType: 'text',
      responseCharset:'utf-8',
      success: function(res) {
        console.log("正常请求" + JSON.stringify(res))
        my.alert({
          content: "正常请求" + JSON.stringify(res)
        })
      },
      fail: function(res) {
        my.alert({
          content: "请求fail" + JSON.stringify(res)
        })
      },
      complete: function(res) {
      }
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 目标服务器 URL。 |
| headers | Object | 否 | 设置请求的 HTTP 头对象，默认 {'content-type': 'application/json'}，该对象里面的 key 和 value 必须是 String 类型。 |
| method | String | 否 | 默认 GET，目前支持 GET/POST/PUT/DELETE。 |
| data | Object / ArrayBuffer | 否 | 详见 **data 参数说明**（ArrayBuffer 在支付宝客户端 10.1.95 或更高版本支持）。 |
| timeout | Number | 否 | 超时时间，单位 ms，默认 30000。 |
| dataType | String | 否 | 期望返回的数据格式，默认 JSON，支持 JSON、text、base64、arraybuffer（10.1.70 版本开始支持）。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### data 参数说明
传给服务器的数据最终会是 String 类型，如果 data 不是 String 类型，会被转换成 String 。转换规则如下：

- 若方法为 `GET`，会将数据转换成 query string： encodeURIComponent(k)=encodeURIComponent(v)&encodeURIComponent(k)=encodeURIComponent(v)...
- 若方法为 `POST` 且 `headers['content-type']` 为 `application/json` ，会对数据进行 JSON 序列化。
- 若方法为 `POST` 且 `headers['content-type']` 为 `application/x-www-form-urlencoded` ，会将数据转换成 query string： encodeURIComponent(k)=encodeURIComponent(v)&encodeURIComponent(k)=encodeURIComponent(v)...

### referer 说明
网络请求的 `referer` Header 不可设置。

`referer` 默认传当前页面的 URL，不支持自定义设置。

其格式固定为 `https://{appid}.hybrid.alipay-eco.com/{appid}/{version}/index.html#pages/index`，其中 `{appid}` 为小程序的 APPID，`{version}` 为小程序发布标识。 

### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | String | 响应数据，格式取决于请求时的 dataType 参数，如果 dataType 值为 base64 时，返回的是符合 [data URI scheme](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs)  规范的内容字符串。 |
| status | Number | 响应码。 |
| headers | Object | 响应头。 |

## 错误码
| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 1 | 请求没有结束，就跳转到了另一个页面。 | <ul><li>建议请求完成后再进行页面跳转。</li><li>如需强行做页面跳转操作，建议加上 RequestTask.abort()  中断请求任务。</li></ul> |
| 2 | 参数错误。 | <ul><li>可能是链接过长导致，建议参数放在 data 中处理。</li><li>建议检查请求时传递的数据是否正常，格式是否正确，可以在请求前打印下入参数据日志。</li></ul> |
| 4/11 | 无权调用该接口。 | <ul><li>没有配置请求白名单导致。检查请求域名是否添加了域名白名单，请预先在 [支付宝小程序管理中心](https://open.alipay.com/mini/dev/list) > 小程序详情页 >**设置** > **开发设置** > **服务器域名白名单** 中配置域名白名单。小程序在以下 API 调用时只能与白名单中的域名进行通讯：HTTP 请求（my.request）、上传文件（my.uploadFile）。域名添加或删除后仅对新版本生效，老版本仍使用修改前的域名配置。</li><li>若是账号问题，不能登录管理后台配置，开发版测试可以先在 IDE 右上角点击 **详情**> **域名信息** 下勾选 **忽略 request 域名合法性检查（仅在本地模拟、预览和远程调试时生效）** 或  **忽略 Webview 域名合法性检查（仅在本地模拟、预览和远程调试时生效）**，再预览调试请求。</li><li>request 请求的地址域名可能写错，导致跟配置的请求白名单域名不一致，请仔细检查。</li></ul> **注意**：添加服务器域名白名单后，一定要发布新版上架，否则会出现异常。 |
| 12 | 网络出错。 | 建议检查网络环境是否正常，服务器是否稳定。 |
| 13 | 超时。 | 建议检查网络环境是否正常，服务器是否正常响应，若请求需要时间长，可适当设置超时时间  timeout。 |
| 14 | 解码失败。 | <ul><li>建议检查前后端请求和响应数据格式是否一致；如：返回数据格式 text 与入参 dataType 值 JSON 不一致而导致接口报错，请修改后台返回数据格式为 JSON。</li><li>如果后端是 PHP 或 .net，可检查响应的内容中是否携带了 bom，清除 UTF-8 bom 头 **。** </li><li>若服务端需要返回非 JSON 字符串，则需要把 my.request 的  dataType 参数设置成 text。</li><li>保证证书链完整且证书不过期。</li></ul> |
| 15 | 传参失败。 | 小程序页面传参如果做 urlencode 需要把整体参数进行编码。 |
| 19 | HTTP 错误。 | <ul><li>请确认请求 URL 地址在外网是否能正常请求，HTTPS 协议，小程序真机上都是线上环境的正式请求，不能使用局域网本地请求。</li><li>一般如 HTTP 404、500、504 等异常错误，建议打开 **IDE 调试器 > Network** 可以查看具体的错误信息，然后根据对应 HTTP 错误码对症处理。</li><li>SSL 证书不正确导致的，建议更换网站 SSL 证书。</li></ul> |
| 20 | 请求已被停止/服务端限流。 | 请确认请求服务器是否能正常请求和响应。 |
|  | 请求 URL 不支持 HTTP，请使用 HTTPS。 | 小程序已经不支持 HTTP 请求，请使用 HTTPS。 |
| 23 | 代理请求失败。 | 建议检查代理配置是否正确。 |

以下几种情况，会返回错误码为 14 的错误（遇到此错误时，请先检查 dataType 的设置是否正确）：

| **入参 dataType 值** | **返回错误码为 14 的原因** |
| --- | --- |
| JSON | 小程序框架对返回结果做 JSON.prase 操作时解析失败。 |
| text | 返回的内容格式不符。 |
| base64 | 转换失败。 |

![|723x75](https://mdn.alipayobjects.com/afts/img/A*vtR5Q7ttYyiX9VBLv1JmVQBkAa8wAA/original?bz=openpt_doc&t=fATCX_-7I4pcMKAl6pUhJAAAAABkMK8AAAAA#align=left&display=inline&height=83&margin=%5Bobject%20Object%5D&originHeight=83&originWidth=800&status=done&style=stroke&width=800)

## 返回值 RequestTask
网络请求任务对象。调用 `my.request` 后返回的请求对象。

### RequestTask.abort()
中断请求任务。调用之后会返回`{"error":9,"errorMessage":"request:fail abort"}`。

### 示例代码
```javascript
// 返回 RequestTask，可以调用 abort 方法取消请求
const task = my.request({url: 'https://httpbin.org/post'})
task.abort();
```
