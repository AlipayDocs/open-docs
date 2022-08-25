# 简介
**my.getRunData** 是获取用户一个自然天内的运动步数信息的 API。目前只支持查询最近 30 天内的运动数据，若超过 30 天，则返回的步数信息为 0。

在开放平台控制台 > 开发设置中配置 **接口内容加密方式** 后，my.getRunData 可获取到加密后的运动数据。开通 [运动数据](https://opendocs.alipay.com/mini/introduce/rundata) 能力并申请用户信息后，在服务端结合签名算法和 AES 密钥对加密后的运动数据进行解密，方法可查看 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3)。

IDE 模拟器暂不支持调试，请以真机调试结果为准。

## 使用限制

- 基础库 [1.17.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.getRunData({
  // 替换为最近三十天内的日期
  countDate: '2022-06-27',
  fail: (res) => {
    console.log('get pedometer encrypted fail:'+JSON.stringify(res))
  },
  success: (res) => {
    let that = this;
    console.log('get pedometer encrypted success:'+JSON.stringify(res))
    my.request({
      // 替换为开发者自己的服务端接口进行解密
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

## 返回示例

返回值 res.response 为完整的报文数据，前端需要将该报文发送到开发者服务端做验签和解密处理（详细的服务端处理流程可查看 **接口内容加密方式**，服务端解密后的明文示例如下：

#### 正常响应
```json
{
    "count": "16880",
    "countDate": "2018-12-19",
    "code": "10000"
}
```

#### 服务端接口异常响应
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

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| countDate | String | 是 | 要查询的步数日期（yyyy-mm-dd）的字符串例如：`countDate: '2018-12-19'` 。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| response | String | 查询到的指定日期的步数，该数据是经过加密的，需要通过 [my.request](https://opendocs.alipay.com/mini/api/owycmh) 请求解密数据。 |

## 结果码
| **结果码** | **描述** | **解决方案** |
| --- | --- | --- |
| MISSING_PARAMETER | 缺少入参信息。 | 检查步数日期是否传入。 |
| INVALID_DATE | 传入的查询日期非法。 | countDate 格式为 yyyy-MM-dd 的字符串，请按照描述修正传入的参数。 |
| INVALID_USER_STATUS | 此用户未开通支付宝运动业务。 | 此支付宝用户未开通支付宝运动业务。<br />需用户在支付宝首页 > **教育公益** > **运动** > **设置** 页面（或直接在支付宝搜索 **运动**）开通支付宝运动业务后才能使用此接口查询用户步数信息。 |
| INVALID_USERID | userid 非法。 | 入参的 userid 格式错误。<br />**注意**: userid 必须是以 2088 开头的 16 位数字字符串，请修正此参数。 |
| INVALID_APP_ID | appId 为空。 | 请检查 appid 是否正确 |

# 常见问题 FAQ

## Q：调用 my.getRunData 为何报错缺少加密配置？
A：未配置应用接口内容加密方式导致的报错。

- 登录支付宝 [开放平台控制台](https://open.alipay.com/dev/workspace) > 选择需要配置的应用，点击进入应用详情页 > **开发** > **开发设置**，配置接口内容加密方式。
- 还可在开放平台控制台 **账户中心** > **密钥管理** > **开放平台密钥** > [接口内容加密方式](https://openhome.alipay.com/dev/workspace/key-manage) 找到需配置的应用，点击 **接口内容加密方式** 对应的 **设置**，配置接口内容加密方式。

两个入口选择其一即可完成配置，详细说明请 [接口内容加密方式](https://opendocs.alipay.com/common/02mse3)。

## Q：服务端解密 my.getRunData 获取的运动数据为何报错 ISV 权限不足？
A：
1. 登录支付宝 [开放平台控制台](https://open.alipay.com/dev/workspace) > 选择需要配置应用，点击进入应用详情页 > **产品绑定** > **绑定产品** > 添加 **运动数据**。
2. 绑定运动数据产品后，在产品绑定页面找到 **运动数据**，点击 **用户信息申请** > 申请 my.queryStepDailyCount 权限，详情可查看 [用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu) > **运动数据**。

![运动数据](https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*9BfURadvtPUAAAAAAAAAAAAAARQnAQ)
![用户信息申请](https://gw.alipayobjects.com/mdn/rms_390dfd/afts/img/A*-PA8QLoNqPQAAAAAAAAAAAAAARQnAQ)
