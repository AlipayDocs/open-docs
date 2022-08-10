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
  content: '模板ext 同步获取结果：' + JSON.stringify(res),
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

A：通常来说，模板小程序通过审核、并且实例化以后，才能在小程序实例中通过 getExtConfig 获取 ext 数据。目前暂未提供相关的调试工具。

考虑模板小程序开发及其实例化的过程中，ext 信息的传递和使用过程：

模板小程序开发：
- 1.1) 服务商创建模板小程序，编码，通过 IDE 在本地调试，完成开发；
- 1.2) 服务商将模板小程序提交审核，支付宝通过审核。

模板小程序实例化：
- 2.1) 服务商服务端调用 alipay.open.mini.version.upload，为特定商户创建模板小程序的实例，传入特定于该商户的 ext 字段；
- 2.2) 支付宝服务端响应 upload 请求，创建小程序新实例/新版本，将 ext 字段保存为 ext.json 文件，置入实例小程序的代码包里（如果模板里就有 ext.json，会被整个覆盖）；
- 2.3) 实例小程序在客户端被加载和运行，它包含与模板小程序一样的前端代码和个性化的 ext.json，前端代码中调用 getExtConfig 正是读取 ext.json 文件，进而实现小程序的个性化配置。

理论上，直到最后一步即 2.3，小程序获取到最终的 ext 信息并且使用。为了尽量避免最后才知道出错，可以将 2.1 开发过程中的 ext 字段的值保存到一个 ext.json 文件，覆盖 1.1 的本地调试环境中的对应文件，测试 getExtConfig 是否能够正确读取，并调试跟它相关的后续前端代码。

## Q：getExtConfigSync 为什么获取不到数据？
A：参考 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 文档
- 检查 alipay.open.mini.version.upload 接口的 `ext` 入参是否是合法的 JSON 字符串。
- 检查 JSON 内容是否符合模板 `ext` 配置规范。
- 检查 JSON 内容中的 `extEnable` 字段是否设置为 `true`。
