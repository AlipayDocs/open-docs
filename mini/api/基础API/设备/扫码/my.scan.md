# 简介
**my.scan** 是调用扫一扫功能的 API。

my.scan 唤起扫一扫前后整个过程会先后执行 app 和 page 的 onHide 和 onShow 生命周期函数。即（唤起）app.onHide > page.onHide >（返回）app.onShow > page.onShow。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/51a1a04f6c0fb75da5344409105c54a4.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/f00386c76c1deff9b8f44c36aec0bff4.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

### .json 示例代码
```json
{
    "defaultTitle": "Scan"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/scan-code/scan-code.axml-->
<view class="page">
  <view class="page-section">
    <form onSubmit="scanCode">
      <view>
        <button type="primary" onTap="scan">扫码</button>
      </view>
    </form>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/scan-code/scan-code.js
Page({
  scan() {
    my.scan({
      scanType: ['qrCode','barCode'],
      success: (res) => {
        my.alert({ title: res.code });
      },
    });
  }
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| scanType | Array | 否 | 扫码识别类型，默认值为 ['qrCode','barCode']。<br />可选值：<br /><ul><li>qrCode：二维码。</li><li>barCode：条码。</li><li>dmCode：DM码。</li><li>pdf417Code：PDF417码。</li><li>narrowCode：窄条二维码。</li><li>hmCode：异构码。</li></ul> |
| hideAlbum | Boolean | 否 | 是否隐藏相册（不允许从相册选择图片），只能从相机扫码。默认值为 false。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| code | String | 扫码所得数据。 |
| qrCode | String | 扫描二维码时返回二维码数据。 |
| barCode | String | 扫描条形码时返回条形码数据。 |
| scanType | String | 码类型。 |
| result | String | 码内容。 |
| imageChannel | String | 来源。 |
| rawData | String | Base64 字节流。 |

## 错误码
| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 10 | 用户取消操作后返回。 | 为用户正常交互流程分支，不需要进行特殊处理。 |
| 11 | 操作失败。 | 具体原因需要查看客户端协助排查。 |

# 常见问题 FAQ
## Q：小程序体验码扫码后为什么页面一直在加载中呢？
A：建议检查下后台配置的域名白名单，首页存在网络请求必须配置白名单。
