# 简介

**my.setTabBarItem** 是动态设置 tabBar 某一项内容（文字、图标）的 API。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器 1.13 及以上版本支持该接口调用。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.setTabBarItem({
  index: 0,
  text: 'text',
  iconPath: '/image/icon-hom.png',
  selectedIconPath: '/image/icon-home-selected.png',
  success(res) {
    console.log('setTabBarItem success');
  },
  fail(res) {
    my.alert({ title: 'setTabBarItem fail', content: JSON.stringify(res) });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| index | Number | 是 | 标签页的项数序号，最左边的为 0，往右顺次增大。 |
| text | String | 是 | 标签页按钮上的文字。 |
| iconPath | String | 否 | 图片路径，建议尺寸为 81px \* 81px，支持 PNG/JPEG/JPG/GIF 图片格式，支持网络图片。<br>对应 app.json 中 tabBar.items[index] 的 icon 属性。 |
| selectedIconPath | String | 否 | 选中时的图片路径，建议尺寸为 81px \* 81px，支持 PNG/JPEG/JPG/GIF 图片格式，支持网络图片。<br>对应 app.json 中 tabBar.items[index] 的 activeIcon 属性。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码

fail 回调会收到一个 Object 类型的参数，其 error 属性为错误码，errorMessage 为错误消息。

| **错误码** | **错误消息** | **解决方案** |
| --- | --- | --- |
| 1 | Currently using customize tabBar. The API [setTabBarItem] does not support! | 自定义的 tabBar 不支持使用 my.setTabBarItem 设置内容。|
| 2 | 无效参数: Error: Index 2 of TabBar do not exists! | 入参 index 超出范围。如果在 app.json 中 tabBar.items 有 n 项，index 应为 0 ~ n-1 |
| 11 | 当前页面不在 tabBar 上。 | 报错原因为 app.json 中未配置 tabBar。请在配置以后再在 tabBar 页面中调用本接口。 |

# Bug & Tip

- `Tip` my.setTabBarBadge() 和 my.setTabBarItem() 同时使用时，有概率会遇到 badge 被遮盖的情况。可通过改为在 setTabBarItem 的 success 回调里调用 setTabBarBadge 解决。
- `Tip` 可使用 [my.setTabBarStyle](https://opendocs.alipay.com/mini/api/wcf0sv) 修改 tabBar 样式。


更多相关问题参见 [tabBar 常见问题](https://opendocs.alipay.com/mini/api/do7urq)。
