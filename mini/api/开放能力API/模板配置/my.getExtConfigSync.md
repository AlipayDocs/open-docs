# 简介
**my.getExtConfigSync** 是 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 中用于获取自定义数据（即 [ext.json](https://opendocs.alipay.com/isv/03kqzl#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 中的 ext 字段）的同步接口。

在模板小程序开发及实例化的过程中，ext 信息的传递路径如下：  

模板小程序开发：   
- 1.1 服务商创建模板小程序并在本地开发，在项目根目录（与 app.json 同级）创建 ext.json 文件，最小示例内容：`{"extEnable":true,"ext":{"i":"am ok"}}`；
- 1.2 服务端对模板小程序进行编码和调试，代码中调用 my.getExtConfig/my.extConfigSync 获取 ext.json 中的 ext 字段内容作为小程序运行时个性化的配置项；
- 1.3 服务商完成模板小程序开发，提交发布，支付宝审核通过。  


模板小程序实例化：   
- 2.1 服务商调用 [alipay.open.mini.version.upload](https://opendocs.alipay.com/isv/03kqzl) 请求为特定商户创建模板小程序实例，传入的 ext 参数包含该商户特有的配置；
- 2.2 支付宝应服务商请求创建小程序新实例或新版本，将请求的 ext 参数保存为 ext.json 文件，置入实例小程序的代码包，覆盖代码包中继承自模板的 ext.json 文件；
- 2.3 小程序实例在客户端被加载运行，它包含与模板小程序一样的代码和个性化的 ext.json，运行时 my.getExtConfig/my.getExtConfigSync 读取此 ext.json 文件中的 ext 字段。

直到最后一步（即 2.3），小程序才能真正获取和使用最终的 ext 信息。这个较晚的时间点会带来一些调试方面的困难，发现相关代码问题往往需要模板小程序重新发布提审。
为了减少反复、节约时间，建议在 1.2 中仔细设计和修改 ext.json，尽可能模拟真实情况并充分调试相关代码，在 2.1 构造真实 ext 内容时严格参照 1.2 中使用的 ext.json 格式。


## 使用限制
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
var res = my.getExtConfigSync();
my.alert({
  content: JSON.stringify(res)
});
```

## 返回值
返回小程序的 `ext.json` 中的 [ext](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 字段的值。

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 20 | 模板配置为空。 | 确保 ext.json 存在（即 alipay.open.mini.version.upload 接口的 ext 参数非空），且其中 ext 字段不为空。 |
| 21 | 已停用模板配置。 | 将 ext.json（即 alipay.open.mini.version.upload 接口的 ext 参数）中 extEnable 字段设置为 true。 |

## Q：为什么实例小程序调用 my.getExtConfig/my.getExtConfigSync 获取不到数据？
A：基本都是 alipay.open.mini.version.upload 传入的 ext 参数有问题，请检查：
- ext 参数内容是否符合模板配置规范（参考 [模板小程序文档](https://opendocs.alipay.com/mini/isv/creatminiapp#ext%20%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E)）；
- ext JSON 内容中 `extEnable` 字段是否已设置为 `true`。
