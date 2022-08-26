# 简介

**my.getExtConfig** 是获取 [小程序模板](https://opendocs.alipay.com/mini/isv/creatminiapp) 自定义数据字段（即 [ext.json](https://opendocs.alipay.com/isv/03kqzl#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 中的 ext 字段）的异步接口。   
在模板小程序开发及实例化的过程中，ext 信息的传递路径如下：   
模板小程序开发：   
- 1.1 服务商创建模板小程序，在本地编码、调试，调试过程中调用 getExtConfig 实质是读取模板项目中的 ext.json 文件中的 ext 字段；
- 1.2 服务商完成开发，将模板小程序提交审核，支付宝通过审核。

模板小程序实例化：   
- 2.1 服务商调用 [alipay.open.mini.version.upload](https://opendocs.alipay.com/isv/03kqzl) 为特定商户创建模板小程序的实例，传入的 ext 参数包含该商户特有的信息；
- 2.2 支付宝响应服务商请求，创建小程序新实例或新版本，将请求的 ext 参数保存为 ext.json 文件置入实例小程序的代码包（代码包中继承自模板的 ext.json 会被覆盖）；
- 2.3 小程序实例在客户端被加载和运行，它包含与模板小程序一样的前端代码和个性化的 ext.json，运行时调用 getExtConfig 实质是读取此 ext.json 文件中的 ext 字段。

理论上，直到最后一步（即 2.3），小程序才能真正获取和使用到最终的 ext 信息。这个较晚的时间点会带来一些调试方面的困难，如果发现前端代码问题需要模板小程序重新发版。
为了提升效率减少反复，建议在 1.1 中使用“假的” ext.json 尽可能地模拟真实情况并充分调试相关代码，在 2.1 构造真实 ext 参数时严格按照 1.1 中 ext.json 的内容格式。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.getExtConfig({
  success: res => {
    my.alert({ content: '模板ext 获取成功：' + JSON.stringify(res.data) });
    console.log({ content: '模板ext 获取成功：' + JSON.stringify(res.data) });
  },
  fail: error => {
    my.alert({ content: '模板ext 获取失败:' + JSON.stringify(error) });
  },
  complete: () => {
    my.alert({ title: '模板ext 获取complete' });
  },
});
```

## 入参

Object 类型，属性如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | Object | 模板 `ext.json` 中的 [ext](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 字段对象。 |

`my.getExtConfig` 的返回值相比 `my.getExtConfigSync` 多了一层 `{ data }` 对象。

## 返回值
返回小程序的 `ext.json` 中的 [ext](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 字段的值。

## 错误码

| **错误码** | **描述**         | **解决方案**   |
| ---------- | ---------------- | -------------- |
| 20         | 模板配置为空。   | 确保 ext.json 存在且 ext 字段不为空。 |
| 21         | 已停用模板配置。 | 将 ext.json 的 extEnable 字段设置为 true。 |

# 常见问题

## Q：为什么实例小程序调用 my.getExtConfig/my.getExtConfigSync 获取不到数据？
A: 一般都是因为 alipay.open.mini.version.upload 传入的 ext 参数有问题，请检查：
- ext 参数内容是否符合模板配置规范（参考 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 文档）；
- ext JSON 内容中 `extEnable` 字段是否已设置为 `true`。

