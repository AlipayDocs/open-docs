# 简介

**my.loadFontFace** 是动态加载网络字体的 API。

目前支持 woff，otf，ttf，sfnt 字体，字体资源地址必须是 https 协议。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 受同源策略限制，字体资源服务器必须开启 CORS 支持。支付宝小程序的域名为 ${appId}.hybrid.alipay-eco.com。
- 字体资源响应头中 Content-Type 请参考本文档附录的 MIME Type。无效的 Content-Type 会导致字体解析失败。

# 接口调用

## 示例代码

### .axml 示例代码

```html
<view class="page">
  <view class="page-description">动态加载网络字体</view>
  <view class="page-section">
    <view class="page-section-title">loadFontFace</view>
    <view class="page-section-demo">
      <button size="default" type="primary" onTap="loadFontFace">
        loadFontFace
      </button>
    </view>
    <view class="custom-web-font"> 自定义字体 </view>
  </view>
</view>
```

### .acss 示例代码

```css
.custom-web-font {
  font-family: 'My Font';
  font-size: 40px;
}
```

### .js 示例代码

```javascript
Page({
  data: {},
  onLoad() {},
  loadFontFace() {
    my.loadFontFace({
      // 替换成自定义的字体和文件
      family: 'My Font',
      source:
        'url("https://gw.alipayobjects.com/os/bmw-prod/b558eecf-5d4f-4481-9e61-ad6fd241857a.ttf")',
      success() {
        my.alert({
          title: 'loadFontFace 成功',
        });
      },
      fail: err => {
        my.alert({
          title: 'loadFontFace 失败',
          content: JSON.stringify(err),
        });
      },
    });
  },
});
```

## 入参

入参为 Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| family | String | 是 | 字体名称。 |
| source | String | 是 | 字体资源地址，格式为 "url('https://...')"，详见示例代码。<br/>**注意：** 字体资源须开启 CORS（Access-Control-Allow-Origin 为 * 或 ${appId}.hybrid.alipay-eco.com），否则 Android 上无法正常加载字体。 |
| desc | Object | 否 | 字体描述符。 |
| global | Boolean | 否 | 加载的字体是否对整个小程序生效。false 表示只在当前页面生效，默认值 `false`。<br>基础库 [2.8.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。 |
| nativeCanvas | Boolean | 否 | 加载的字体是否在 native canvas （即 axml 中指定了 type 属性的 \<canvas\>）中可用，默认值 `true`。<br>基础库 [2.6.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### desc 结构

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| style | String | 否 | 字体样式，默认值为 normal，可选值为 normal / italic / oblique。 |
| weight | String | 否 | 字体粗细，默认值为 normal，可选值为 normal / bold / 100 / 200 / ... / 900。 |
| variant | String | 否 | 设置小型大写字母的字体显示文本，默认值为 normal，可选值为 normal / small-caps / inherit。 |

## 错误码

fail 回调会收到的 Object 类型的参数，其 error 属性为错误码，errorMessage 属性为错误消息。

| **错误码** | **错误消息** | **解决方案**                          |
| ---------- | -------- | ------------------------------------- |
| 10         | 加载失败 | 请检查字体链接是否为有效的 HTTPS 链接，字体链接是否开启了 CORS 支持，字体格式及 Content-Type 是否有效。 |

# 常见问题 FAQ

## Q：my.loadFontFace 支持加载 woff2 字体吗？
A：支付宝小程序不支持加载 woff2 字体。相对其他格式字体，woff2 字体内存占用较高，建议使用其他格式。

# 附录
my.loadFontFace 所支持字体格式的 MIME Type
| **字体** | **MIME Type** |
| ---------- | -------- |
| woff         | font/woff |
| otf         | font/otf |
| ttf         | font/ttf |
| sfnt         | font/sfnt |
