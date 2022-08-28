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
| USER_DATA_PATH | String | 文件系统中的用户目录路径（本地路径）。<br />基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持。 |
| clientName | String | 客户端名称简写。<br />支付宝客户端为 <code>'ap'</code>。<br />基础库 <b>1.24.9</b> 开始支持。 |
| clientVersion | String | 客户端版本号。例如 <code>"10.2.6"</code>。<br />基础库 <b>1.24.9</b> 开始支持。 |
| language | String | 设置的语言。<br /> <ul><li>zh-Hans：简体中文。</li><li>en：英文。</li><li>zh-HK：繁体中文-香港。</li><li>zh-Hant：繁体中文-台湾。</li></ul>基础库 <b>1.24.9</b> 开始支持。 |
| platform | String | 系统名称。<br /><ul><li>iOS：iOS 系统。</li><li>Android：安卓系统。</li><li>unknown：未知系统。</li></ul>基础库 <b>1.24.9</b> 开始支持。 |
