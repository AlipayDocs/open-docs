# 简介
预拉取能够在小程序冷启动的时候客户端向第三方服务器拉取业务数据，当页面打开时来获取数据可以更快地渲染页面，减少用户等待时间，从而提升小程序的打开速度 。

## 使用限制

- 支付宝客户端 10.2.36 版本，基础库 [2.7.11](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 使用流程

## 配置文件
在小程序开发者工具 IDE 根目录创建 preload.json（自研小程序），该文件中填写预加载配置。

**注意**：

- preload.json 最多支持配置 2048 个字节，超过大小IDE会提示超限。
- 模板实例化小程序的场景使用 ext 设置（见后面的配置说明）。

![](https://intranetproxy.alipay.com/skylark/lark/0/2021/png/185602/1632191030970-c4309ca7-edad-4f44-8e98-b73a5024b2ab.png#align=left&display=inline&height=313&margin=%5Bobject%20Object%5D&originHeight=313&originWidth=218&status=done&style=none&width=218)

### 属性说明
| **属性** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |
| fetchType | String | 否 | 请求类型。目前只支持 pre。<br />**默认值：** pre. |
| params | Object | 是 | 解析配置的请求 |


#### params 对象属性说明
| **属性** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |
| url | String | 是 | 请求 URL。 |
| method | String | 否 | HTTP 请求方法。支持 GET、POST、DELETE、PUT。<br />**默认值：** GET。 |
| headers | Array | 否 | 自定义请求头。 |
| dataType | String | 否 | 期望返回的数据格式。支持 JSON、text、base64、arraybuffer。<br /> **默认值：** JSON。 |
| data | Object | 否 | 请求的参数。<br /><ul><li>如果是 method 为 GET，会将参数做成 query拼接在 url 后。</li><li>如果 method 为 POST，将默认以 x-www-form-urlencoded 提交。</li></ul> |

### 配置示例

#### 自研小程序在 preload.json 配置
**注意：** 实际的配置文件不支持注释，下面文件中的注释部分只是为了更好说明每个字段的作用，请在拷贝的时候从配置文件中删除。
```objectivec
[
  {
    "fetchType": "pre",  //配置pre
    "params": {
      "url": "https://*****",  //http请求的URL地址
      "method": "POST", // http method，支持GET/POST/DELETE/PUT
      "data": {       //可选。请求的参数，如果是method为GET，会将参数做成query拼接在url后
        "foo": "bar"
      },
      "headers": { //可选。额外的header信息。
      	"token":"xxx"
      },
      "dataType": "json"   //期望返回的数据格式，默认 JSON，支持 JSON、text、base64、arraybuffer
    }
  }
]
```

#### 模板小程序实例化时 ext 配置
如果同时在 ext 和 preload.json 配置，会优先读取 ext 的配置，如果 ext 没有配置，则读取 preload.json 的配置。<br />实际的配置文件不支持注释，下面文件中的注释部分只是为了更好说明每个字段的作用，请在拷贝的时候从配置文件中删除。
```json
"preload":
[
  {
    "fetchType": "pre",  //配置pre
    "params": {
      "url": "https://*****",  //http请求的URL地址
      "method": "POST", // http method，支持GET/POST/DELETE/PUT
      "data": {       //可选。请求的参数，如果method为GET，会将参数做成query拼接在url后
        "foo": "bar"
      },
      "headers": { //可选。额外的header信息。
      	"token":"xxx"
      },
      "dataType": "json"   //期望返回的数据格式，默认 JSON，支持 JSON、text、base64、arraybuffer
    }
  }
]
```

## 请求数据
当用户打开小程序时，客户端会发起一个 http request，其中包含的 query 参数如下，数据获取到后会将整个 HTTP body 缓存到本地。

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| appId | String | 小程序的 APPID。 |
| timestamp | Long | 请求发起的时间戳。 |

除上述字段外还包括 preload.json 配置文件中 data 的数据，例如以下参数：
| **参数** | **类型** | **描述** |
| --- | --- | --- |
| foo | String | 业务自定义参数，key 和 value 为配置文件中的对应值 {"foo":"bar"}。 |

## 获取数据
通过调用 JSAPI getBackgroundFetchData  获取预加载的数据：
```typescript
my.getBackgroundFetchData({
	fetchType: "pre",
  success(res) {
  	console.log(res.fetchedData);
  },
  fail(res) {
  	console.log("getBackgroundFetchData fail: ", res)
  }
})
```

### 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| fetchType | String | 是 | 请求类型。<br />暂时只支持 pre。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| fetchType | String | 当前请求类型，目前只支持 pre。 |
| timestamp | Number | 客户端拿到缓存数据的时间戳。 |
| fetchedData | Object | 当前预加载的 response 数据。 |

### 错误码
| **错误码** | **说明** |
| --- | --- |
| 2 | 参数错误 |
| 3 | 没有预加载数据 |
