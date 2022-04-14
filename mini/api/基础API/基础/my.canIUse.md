
# 简介
**my.canIUse** 是判断当前小程序的 API、入参或返回值、组件、属性等在当前版本是否支持的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用
## 示例代码
### .js 示例代码

```javascript
// 新增 API 是否可用
my.canIUse('getFileInfo')
// API 新增属性是否可用
my.canIUse('closeSocket.object.code')
// API 新增属性是否可用
my.canIUse('getLocation.object.type')
// API 返回值新增属性是否可用
my.canIUse('getSystemInfo.return.brand')
// 新增组件「关注生活号」是否可用
my.canIUse('lifestyle')
// 组件新增属性值是否可用
my.canIUse('button.open-type.share')
```

## 入参
参数使用 `${API}.${type}.${param}.${option}` 或者 `${component}.${attribute}.${option}` 方式来调用。

- API 表示 API 的名称，不包括 my. 的名称。例如：想判断 my.getFileInfo，只需传入 getFileInfo 即可。
- type 取值 object/return/callback，表示 API 的判断类型。
- param 表示参数的某一个属性名。
- option 表示参数属性的具体属性值。
- component 表示组件名称。
- attribute 表示组件属性名。
- option 表示组件属性值。

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| 是否支持 | Boolean | true 表示支持，false 表示不支持。 |
