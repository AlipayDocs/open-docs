
# 简介
**my.getExtConfigSync** 是获取 [模板小程序](https://opendocs.alipay.com/mini/isv/creatminiapp#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E) 自定义数据字段的同步接口。

## 使用限制
此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
var res = my.getExtConfigSync();
my.alert('模板ext 同步获取结果：' + JSON.stringify(res));
```

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | Object | 模板 `ext.json` 中的 ext 字段对象。 |


## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 20 | 模板配置为空。 | 检查模板配置。 |
| 21 | 已停用模板配置。 | 启用模板配置。 |

