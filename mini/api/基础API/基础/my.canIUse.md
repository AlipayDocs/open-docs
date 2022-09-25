# 简介

**my.canIUse** 是判断小程序的 API、入参或返回值、组件、属性等是否在当前版本可用的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 接口 getFileInfo 是否可用
my.canIUse('getFileInfo');
// 接口 closeSocket 是否有返回值
my.canIUse('closeSocket.return');
// 接口 closeSocket 的入参是否包含 code
my.canIUse('closeSocket.object.code');
// 接口 getLocation 的返回值是否包含 type
my.canIUse('getLocation.return.type');
// 接口 getSystemInfo 的回调中是否包含 brand
my.canIUse('getSystemInfo.callback.brand');

// 组件 lifestyle（关注生活号）是否可用
my.canIUse('lifestyle');
// 组件 button 是否包含 open-type 属性
my.canIUse('button.open-type');
// 组件 button 的 open-type 属性的值是否可以为 share
my.canIUse('button.open-type.share');
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

| **类型** | **描述**                          |
| -------- | --------------------------------- |
| Boolean  | 当前版本是否可用，true 表示可用，false 表示不可用。 |
