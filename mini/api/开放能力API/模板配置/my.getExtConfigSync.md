# 简介
**my.getExtConfigSync** 是获取 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 自定义数据字段的同步接口。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。本接口支持使用 [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use) 接口判断是否支持。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
var res = my.getExtConfigSync();
my.alert({
  content: '模板ext 同步获取结果：'+JSON.stringify(res),
  buttonText: 'OK'
});
```

## 返回值
返回模板 `ext.json` 中的 [ext](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 字段的值。

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 20 | 模板配置为空。 | 检查模板配置。 |
| 21 | 已停用模板配置。 | 启用模板配置。 |

## Q：为什么获取不到数据
A：参考 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 文档
- 检查接口 `ext` 入参是否是合法 `json` 字符串，且内容符合模板 `ext` 配置规范。
- 检查 `extEnable` 的值是否设置为 `true`。
