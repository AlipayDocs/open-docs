# 简介
**my.getExtConfigSync** 是获取 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 自定义数据字段的同步接口。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。

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

# 常见问题 FAQ

## Q：我是服务商开发者，我这边开发了一个模板小程序，并且注入了扩展的 json 文件，请问我如何判断我授权的商户是否可以拿到 ext 参数呢？请问在不通过商户调用的情况下，我怎么能在服务商端确定我授权商户小程序中能拿到这个ext数据，有没有工具可以调试?
A：在确保字段是合法且正确的基础上，上传当前模板小程序，然后等待审核通过后，就可以通过 [my.getExtConfig()](https://opendocs.alipay.com/mini/api/getExtConfig) 或 [my.getExtConfigSync()](https://opendocs.alipay.com/mini/api/getExtConfigSync)获取 ext 参数内容；
目前没有相关的调试工具可以在未通过审核的情况下就可以获取 ext 参数。

## Q：为什么获取不到数据？
A：参考 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 文档
- 检查接口 `ext` 入参是否是合法 `json` 字符串，且内容符合模板 `ext` 配置规范。
- 检查 `extEnable` 的值是否设置为 `true`。
