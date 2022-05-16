
# 简介

**my.canIUse** 是判断当前小程序的 API、入参或返回值、组件、属性等在当前版本是否支持的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用
## 示例代码
### .js 示例代码

```javascript
// getFileInfo 接口是否可用
my.canIUse('getFileInfo')
// closeSocket 接口的参数是否包含 code
my.canIUse('closeSocket.object.code')
// getLocation 接口的参数是否包含 type
my.canIUse('getLocation.object.type')
// getSystemInfo 接口的返回值是否包含 brand
my.canIUse('getSystemInfo.return.brand')
// 组件 lifestyle（关注生活号）是否可用
my.canIUse('lifestyle')
// button 组件的 open-type 属性的值是否可以为 share
my.canIUse('button.open-type.share')
```

## 入参

如果想判断 API 是否可用，入参需要形如 `${API}.${type}.${param}.${option}`：

- API 表示 API 的名称，不包括 my. 的名称。例如：想判断 my.getFileInfo，只需传入 getFileInfo 即可。
- type 取值 object/return/callback，表示 API 的判断类型。
- param 表示参数的某一个属性名。
- option 表示参数属性的具体属性值。

如果想判断组件是否可用，入参需要形如 `${component}.${attribute}.${option}`：

- component 表示组件名称。
- attribute 表示组件属性名。
- option 表示组件属性值。

## 返回值

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| 是否支持 | Boolean | true 表示支持，false 表示不支持。 |
