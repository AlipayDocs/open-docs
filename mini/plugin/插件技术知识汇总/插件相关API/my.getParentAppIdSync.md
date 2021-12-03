
# 简介
my.getParentAppIdSync 用于在插件中获取小程序的 appId。

**版本要求**： 基础库 1.21.0 开始支持，低版本需做 [兼容处理](/mini/framework/compatibility)。

# 返回值
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| appId | String | 使用该插件的小程序 appId。 |


# 示例代码
```javascript
const appIdRes = my.getParentAppIdSync();
console.log(appIdRes.appId);
```

# 相关文档
[开发插件](https://opendocs.alipay.com/mini/plugin/plugin-development)
