
# 简介
**my.setTabBarItem** 是动态设置标签页（tabbar）某一项的内容的 API。

相关问题请参见 [tabBar 常见问题](/mini/api/do7urq)。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- IDE 模拟器 1.13 及以上版本支持该接口调用。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```
//  .js
my.setTabBarItem({
    index: 0,
    text: 'text',
    iconPath: '/image/iconPath',
    selectedIconPath: '/image/selectedIconPath'
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| index | Number | 是 | 标签页的项数序号，从左边开始计数。 |
| text | String | 是 | 标签页按钮上的文字。 |
| iconPath | String | 是 | 图片路径，建议尺寸为 81px * 81px，支持 png/jpeg/jpg/gif 图片格式，支持网络图片。 |
| selectedIconPath | String | 是 | 选中时的图片路径，建议尺寸为 81px * 81px，支持 png/jpeg/jpg/gif 图片格式，支持网络图片。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

