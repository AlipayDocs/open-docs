# 简介
**my.getExtConfig** 是获取 [小程序模板](https://opendocs.alipay.com/mini/isv/creatminiapp) 自定义数据字段的异步接口。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.getExtConfig({
  success: (res) => {
    my.alert({ content: '模板ext 获取成功：' + JSON.stringify(res.data), });
    console.log({ content: '模板ext 获取成功：' + JSON.stringify(res.data), });
  },
  fail: (error) => {
    my.alert({ content: '模板ext 获取失败:' + JSON.stringify(error), });
  },
  complete: () => {
    my.alert({ title: '模板ext 获取complete', });
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

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 20 | 模板配置为空。 | 检查模板配置。 |
| 21 | 已停用模板配置。 | 启用模板配置。 |

# 常见问题

## Q：为什么获取不到数据
A：参考 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 文档
- 检查接口 `ext` 入参是否是合法 `json` 字符串，且内容符合模板 `ext` 配置规范。
- 检查 `extEnable` 的值是否设置为 `true`。
