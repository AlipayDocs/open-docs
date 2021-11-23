
# 简介
**my.getRunData** 是获取用户一个自然天内的运动步数信息的 API。详情可参见 [运动数据](https://opendocs.alipay.com/mini/introduce/rundata) 能力介绍。

调用本 API 时无需再接入授权 API，系统将自动会检查用户是否已授权。若用户尚未授权，则会弹出授权框；用户同意授权后，可获取到返回的加密数据。 然后在服务端结合签名算法和 AES 密钥进行解密，获取运动数据，方法详见 [敏感信息加解密方法](https://opendocs.alipay.com/mini/introduce/aes)。

## 使用限制

- 目前只支持查询最近 30 天内的运动数据，若超过 30 天，则返回的步数信息为 0。
- 基础库 [1.17.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.getRunData({
  countDate: '2018-12-19',
  fail: (res) => {
    console.log('get pedometer encrypted fail:'+JSON.stringify(res))
  },
  success: (res) => {
    let that = this;
    console.log('get pedometer encrypted success:'+JSON.stringify(res))
    my.request({
      url: 'http://www.telmo.cn/gateway/decrypt',
      data: {
        encryptContent: res.response
      },
      success: function(res) {
        console.log('decrypt pedometer success:'+JSON.stringify(res))
        that.setData({
          step: res.data.count
        })
      },
      fail: function(res) {
        console.log('decrypt pedometer fail:'+JSON.stringify(res))
      }
    })
  },
  complete: (res) => {
    console.log('getRunData complete:' + JSON.stringify(res))
  }
})
```

## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| countDate | String | 是 | 要查询的步数日期（yyyy-mm-dd）的字符串例如：`countDate: '2018-12-19'` 。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| response | String | 查询到的指定日期的步数，该数据是经过加密的，需要通过 [my.request](https://opendocs.alipay.com/mini/api/owycmh) 请求解密数据。 |

res.response 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理（详细的服务端处理流程参考 [敏感信息加解密方法](https://opendocs.alipay.com/mini/introduce/aes)），服务端解密后的明文示例如下：

### 正常响应
```json
{
    "count": "16880",
    "countDate": "2018-12-19",
    "code": "10000"
}
```

### 服务端接口异常响应
```json
{
    "code": "40003",
    "msg": "Insufficient Conditions",
    "subCode": "isv.invalid-auth-relations",
    "subMsg": "无效的授权关系"
}
{
    "code": "20000",
    "msg": "Service Currently Unavailable",
    "subCode": "aop.unknow-error",
    "subMsg": "系统繁忙"
}
{
    "code": "40001",
    "msg": "Missing Required Arguments",
    "subCode": "isv.missing-default-signature-type",
    "subMsg": "应用未设置默认签名类型"
}
//解决方案：重新保存下开发者的密钥，或者设置下小程序的应用网关地址
{
    "code": "40002",
    "msg": "Invalid Arguments",
    "subCode": "isv.invalid-encrypt",
    "subMsg": "加密异常"
}
//解决方案：按文档重新设置AES密钥
```

## 结果码
| **结果码** | **描述** | **解决方案** |
| --- | --- | --- |
| MISSING_PARAMETER | 缺少入参信息。 | 检查步数日期是否传入。 |
| INVALID_DATE | 传入的查询日期非法。 | countDate 格式为 yyyy-MM-dd 的字符串，请按照描述修正传入的参数。 |
| INVALID_USER_STATUS | 此用户未开通支付宝运动业务。 | 此支付宝用户未开通支付宝运动业务。<br />需用户在支付宝首页 > **教育公益** > **运动** > **设置** 页面（或直接在支付宝搜索 **运动**）开通支付宝运动业务后才能使用此接口查询用户步数信息。 |
| INVALID_USERID | userid 非法。 | 入参的 userid 格式错误，请注意: userid 必须是以 2088 开头的 16位数字字符串 请修正此参数 |
| INVALID_APP_ID | appId 为空。 | 请检查 appid 是否正确 |


## 常见问题 FAQ

### Q：安卓系统下的用户在未开启 my.getRunData 时，调用这个方法为何报错：SYNC getAPPInfo do not execute callback？
A：这是已知问题，会在基础库 **1.23.0** 版本修复，原因是同步 API 容器底层偶现异常导致，具体发布可以关注官网的 [基础库更新日志](/mini/ide/framework-changelog)。

### Q：调用 my.getRunData 运动数据为何报错缺少加密配置？
A：未配置开放平台 AES 密钥导致的报错。

1. 登录支付宝 [开放平台](https://open.alipay.com/platform/home.htm) ，在 **管理中心** 选择需要配置 AES 密钥的应用，在 **应用详情** > **应用环境** 页面配置 AES 密钥。<br />
1. 在开放平台，**账户密钥管理** 页面点击配置 AES 密钥。<br />

两个入口选择其一即可完成配置，详细说明请 [点此查看](https://docs.open.alipay.com/common/104567)。
