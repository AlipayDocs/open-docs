# 简介

**my.loadFontFace** 是动态加载网络字体的 API，默认支持在 Canvas 2D 下使用。

目前支持 woff，otf，ttf，sfnt 字体，字体文件地址必须是 https 协议。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 字体链接必须是同源下的，或开启了 cors 支持。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

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
// .js
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
          title: 'loadfontface 成功!!!',
        });
      },
      fail: err => {
        my.alert({
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
| global | Boolean | 否 | 是否全局生效。<br/>默认值 `false`。</br>[2.8.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。 |
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

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**                                              |
| -------- | -------- | ----------------------------------------------------- |
| status   | String   | 加载字体结果。loaded 表示加载成功，error 表示加载失败 |

## 错误码

| **错误码** | **描述** | **解决方案**                          |
| ---------- | -------- | ------------------------------------- |
| 10         | 加载失败 | 检查字体文件是否为可下载的 https 链接 |

# 常见问题 FAQ

## Q：my.loadfontface 支持加载 woff2 字体吗？

A：支付宝小程序不支持 woff2 字体。相对其他格式字体，woff2 字体内存占用较高，建议使用其他格式。

## Q：my.loadfontface 在IDE不生效？
A：my.loadfontface 只会在真机环境有作用，在IDE环境会报错。

## Q：为什么 my.loadfontface 双端表现不一致，iOS 加载成功，安卓加载失败？
A：安卓和 iOS 策略不一致导致的，安卓要求字体资源必须是同源下的。解决方式是需要后端配置跨域 'Access-Control-Allow-Origin': '*'。
