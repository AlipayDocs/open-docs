# 简介
**my.getRunData** 是获取用户某一个自然天内运动步数的 API。目前只支持查询最近 30 天内的运动步数，若超过 30 天，则返回的步数为 0。

此 API 是运动数据产品的一部分，调用之前请确保完成以下步骤：

**第一步**：绑定 **运动数据** 产品并登录 **主账号** 进行 **用户信息申请**。登录支付宝 [开放平台控制台](https://open.alipay.com/dev/workspace) -> 选择需要配置的小程序，点击进入详情页 -> **产品绑定** -> **绑定产品**，选择 **运动数据** 并添加 -> 回到产品绑定页面，找到 **运动数据**，点击 **用户信息申请**，申请 my.queryStepDailyCount 权限。如果申请用户信息按钮为灰色，请检查小程序是否设置主营行业，并且对照以下文档检查应用是否符合主营行业及字段使用场景的要求：[用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu) 。

**第二步**：配置接口加签方式以及接口内容加密方式。配置有以下两个入口：
- 登录支付宝 [开放平台控制台](https://open.alipay.com/dev/workspace) -> 选择需要配置的小程序，点击进入详情页 -> 开发设置 -> 点击 **接口内容加密方式、接口加签方式** 对应的 **设置**，按照页面指引进行配置即可。
- 登录支付宝 [开放平台控制台](https://open.alipay.com/dev/workspace) > **账户中心** > **密钥管理** > [**开放平台密钥**](https://openhome.alipay.com/dev/workspace/key-manage) > 找到需要配置的小程序 > 点击 **接口内容加密方式、接口加签方式** 对应的 **设置**，按照页面指引进行配置即可。

以上两步均完成之后，调用 my.getRunData 可以获取到加密后的运动数据，通过网络请求（如 my.request）将加密数据传给开发者服务端，开发者服务端使用 [AES 密钥](https://opendocs.alipay.com/common/02mse3) 对加密后的运动数据进行解密，获取到运动步数数据。为确保数据完整性，开发者服务端也可通过 [签名算法](https://opendocs.alipay.com/common/02mriz) 对所收到的数据进行验签。

## 使用限制

- 基础库 [1.17.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.60 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。

# 接口调用
## 示例代码
```javascript
my.getRunData({
  // 替换为最近三十天内某一天的日期
  countDate: '2022-06-27',
  fail: res => {
    console.log('get pedometer encrypted fail:' + JSON.stringify(res));
  },
  success: res => {
    console.log('get pedometer encrypted success:' + JSON.stringify(res));
    // 如果 response 为 String 类型 则为加密报文
    // 如果 response 为 Object 类型且抛出异常信息，则为加密异常
    const { response = '' } = res;
    if(typeof response === 'string') {
      my.request({
        // 替换为开发者自己的服务端接口进行解密
        url: 'http://www.telmo.cn/gateway/decrypt',
        data: {
          encryptContent: response,
        },
        success: function (res) {
          console.log('decrypt pedometer success:' + JSON.stringify(res));
        },
        fail: function (res) {
          console.log('decrypt pedometer fail:' + JSON.stringify(res));
        },
      });
    } else {
      // 根据错误信息进行排查
      my.alert({ message: JSON.stringify(response) });
    }
  },
  complete: res => {
    console.log('getRunData complete:' + JSON.stringify(res));
  },
});
```
## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| countDate | String | 是 | 要查询的步数日期（yyyy-mm-dd）的字符串例如：`countDate: '2018-12-19'`。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## success 回调返回值
Object 类型，参数如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| response | String / Object   | 如果返回值为 String 类型，则为 **经过加密的指定日期的步数数据**，需要通过 [my.request](https://opendocs.alipay.com/mini/api/owycmh) 请求解密运动数据。<br /> 如果为 Object 类型且返回异常报错信息，则为加密异常。 |

#### 加密异常 response 返回异常信息
数据格式如下：
```json
{
  "code": "40003",
  "msg": "Insufficient Conditions",
  "subCode": "isv.invalid-auth-relations",
  "subMsg": "无效的授权关系"
},
```
错误码穷举如下：
| 系统级错误码（code） | 系统级错误描述（msg） | 业务级错误码（subCode） | 业务级错误描述（subMsg） | 解决方案 |
| --- | --- | --- | --- | --- |
| 20000 | Service Currently Unavailable | aop.unknow-error | 系统繁忙。 | 稍后再试。 |
| 40001 | Missing Required Arguments  | isv.missing-encrypt-key | 缺少加密配置 | 按照简介说明配置 **接口内容加密方式** |
| 40001 | Missing Required Arguments | isv.missing-default-signature-type" | 应用未设置默认签名类型 | 重新保存下开发者的密钥，或者设置下小程序的应用网关地址 |
| 40002 | Invalid Arguments  | isv.invalid-encrypt | 加密异常。 | 按文档重新设置AES密钥。 |

## 开发者服务端解密 
### 解密成功
数据格式如下：
```json
{
  "count": 16880,
  "countDate": "2018-12-19",
  "code": "10000"
  "msg": "Success"
}
```
### 解密异常
数据格式如下： 
```json
{
    "code": "40003",
    "msg": "Insufficient Conditions",
    "subCode": "isv.invalid-auth-relations",
    "subMsg": "无效的授权关系"
},
```
错误码穷举如下：

| 系统级错误码（code） | 系统级错误描述（msg） | 业务级错误码（subCode） | 业务级错误描述（subMsg） | 解决方案 |
| --- | --- | --- | --- | --- |
| 40006 | Insufficient Permissions | isv.insufficient-isv-permissions | ISV权限不足，建议在开发者中心检查签约是否已经生效。 | 小程序产品绑定。登录支付宝 [开放平台控制台](https://open.alipay.com/dev/workspace) -> 选择需要配置的小程序，点击进入详情页  -> 产品绑定 -> 找到 **运动数据**，点击 **用户信息申请**，申请 my.queryStepDailyCount 权限，申请规则可查看 [用户信息申请及使用基础规则](https://opendocs.alipay.com/common/02kkuu) 。 |

## Fail 回调返回值
| 错误码 | 说明 | 解决方案 |
| --- | --- | --- |
| 2 | 接口参数无效 | 请检查入参是否正确传入。 |
| 1003 | 未授权支付宝应用计步权限 | 为用户拒绝计步授权，无需进行特殊处理。 |
| 1005 | 用户未开通支付宝运动功能 | 引导用户按照以下步骤开通：支付宝 APP 首页 **更多** 进入到应用中心页面，找到 **教育公益** 下**运动**，按照页面指引，点击 **同意协议并允许授权** 即可。 |



