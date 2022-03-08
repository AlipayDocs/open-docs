
# 简介
**my.loadFontFace** 是动态加载网络字体的 API。

## 使用限制

- 文件地址需为下载类型。
- iOS 仅支持 HTTPS 格式文件地址。
- 支付宝小程序目前只支持 woff，otf，ttf，sfnt 字体。
- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 支付宝小程序不支持 woff2 字体，原因是：
   - 相对其他格式字体，对内存占用较高。
   - 此字体支持对于内核 so size 有较大负担，目前支付宝使用的 u4 内核 3.0 将 woff2 格式支持给裁剪了，导致无法正常显示， 建议使用其他格式。

# 接口调用

## 示例代码

### .axml 示例代码
```html
<!-- .axml -->
<view class="page">
  <view class="page-description">动态加载网络字体</view>
  <view class="page-section">
    <view class="page-section-title">loadFontFace</view>
    <view class="page-section-demo">
      <button size="default" type="primary" onTap="loadFontFace">
        loadFontFace
      </button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// .js
Page({
  data: {},
  onLoad() { },
  loadFontFace() {
    my.loadFontFace({
      family: 'Bitstream Vera Serif Bold',
      source: 'url("https://sungd.github.io/Pacifico.ttf")',
      success() {
        my.alert({
          title: 'loadfontface 成功!!!',
        })
      },
      fail: (err) => {
        my.alert({
          content: JSON.stringify(err),
        })
      },
    })
  },
})
```

## 入参
入参为 Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| global | Boolean | 否 | 是否全局生效。<br/>默认值 `false`。</br>[2.7.15](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)开始支持。 |
| family | String | 是 | 字体名称。 |
| source | String | 是 | 字体资源地址。 |
| desc | Object | 否 | 字体描述符。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### desc 结构
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| style | String | 否 | 字体样式，默认值为 normal，可选值为 normal / italic / oblique。 |
| weight | String | 否 | 字体粗细，默认值为 normal，可选值为 normal / bold / 100 / 200../ 900。 |
| variant | String | 否 | 设置小型大写字母的字体显示文本，默认值为 normal，可选值为 normal / small-caps / inherit。 |

