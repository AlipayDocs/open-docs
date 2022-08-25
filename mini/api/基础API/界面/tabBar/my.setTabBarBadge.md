# 简介

**my.setTabBarBadge** 是为标签页（tabbar）某一项的右上角添加文本的 API。可用于设置消息条数的红点提醒。

相关问题请参见 [tabBar 常见问题](https://opendocs.alipay.com/mini/api/do7urq)。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器 1.13 及以上版本支持该接口调用。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 效果示例

![|600x338](https://cdn.nlark.com/yuque/0/2021/png/179989/1624861413254-5f992f28-1928-4e88-9ed8-b2c07be7ac6e.png#align=left&display=inline&height=338&margin=%5Bobject%20Object%5D&name=my.setTabBarBadge.png&originHeight=720&originWidth=1280&size=73740&status=done&style=none&width=600)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.setTabBarBadge({
  index: 0,
  text: '42',
  success(res) {
    console.log(res);
  },
  fail(res) {
    console.log('setTabBarBadge fail: ', res);  
  }
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| index | Number | 是 | 标签页的项数序号，从左边开始计数。 |
| text | String | 是 | 显示的文本，超过三个字符则显示前两个字符+“…”。<br />例如：“支付宝”显示“支付宝”，“蚂蚁集团”显示“蚂蚁…”。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码
fail 回调会收到一个 Object 类型的参数，其 error 属性为错误码，errorMessage 为错误消息。

| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 2 | 无效参数: Error: Index 5 of TabBar do not exists!  | 入参 index 超出范围。如果在 app.json 中 tabBar.items 有 n 项，index 应为 0 ~ n-1 |

