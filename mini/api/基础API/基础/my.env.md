
# 简介
**my.env** 是小程序环境变量对象 API。

对比 [my.getSystemInfo](https://opendocs.alipay.com/mini/api/system-info) / [my.getSystemInfoSync](https://opendocs.alipay.com/mini/api/gawhvz)，my.env 在使用上更加轻量化。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
if (my.canIUse('env')) {
  console.log(my.env.USER_DATA_PATH);
}
if (my.canIUse('env.clientName')) {
  console.log(my.env);
}
```

## 属性
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| USER_DATA_PATH | String | 文件系统中的用户目录路径 (本地路径)。<br />基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持。 |
| clientName | String | 客户端名称简写。<br />支付宝客户端为 'ap'。<br />基础库 [1.24.9](https://opendocs.alipay.com/mini/framework/lib) 开始支持。 |
| clientVersion | String | 客户端版本号。例如"10.2.6"。<br />基础库 [1.24.9](https://opendocs.alipay.com/mini/framework/lib) 开始支持。 |
| language | String | 设置的语言。<br /> <ul><li>简体中文："zh-Hans"。</li><li>英文："en"。</li><li>繁体中文-香港："zh-HK"。</li><li>繁体中文-台湾："zh-Hant"。</li></ul>基础库 [1.24.9](https://opendocs.alipay.com/mini/framework/lib) 开始支持。 |
| platform | String | 系统名称。<br /><ul><li>iOS 系统：'iOS'。</li><li>安卓系统：'Android'。</li><li>未知系统：'unknown'。</li></ul>基础库 [1.24.9](https://opendocs.alipay.com/mini/framework/lib) 开始支持。 |

