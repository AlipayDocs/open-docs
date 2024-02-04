# 简介

图片。支持 JPG、PNG、SVG、WEBP、GIF 等格式。

## 使用限制

使用 webview 嵌套 H5 时，若遇到图片资源不显示的问题，可查看[配置 H5 白名单流程](https://opendocs.alipay.com/mini/component/idfvg6)获取 H5 页面中所有的域名地址（含图片静态资源的地址），全部加入域名白名单中。

## 扫码体验

![图片示例](https://gw.alipayobjects.com/zos/skylark-tools/public/files/66539db61b570eb2b7cf2df4241ea56c.png)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/image/index&defaultOpenedFiles=pages/image/index&theme=light)
## 属性说明

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| src | String | 图片地址。 |
| mode | String | 图片模式。默认值：`scaleToFill`。 |
| class | String | 外部样式。 |
| style | String | 内联样式。 |
| lazy-load | Boolean | 支持图片懒加载，不支持通过 CSS 来控制 image 展示隐藏的场景。默认值：`false`。版本要求：基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。 |
| default-source | String | 默认图片地址，若设置默认图片地址，会先显示默认图片，等 src 对应的图片加载成功后，再渲染对应的图片。版本要求：基础库 [1.19.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上。 |
| onLoad | EventHandle | 图片载入完毕时触发，事件对象 `event.detail = {height: '图片高度px', width: '图片宽度px'}`。 |
| onError | EventHandle | 当图片加载错误时触发，事件对象 `event.detail = {errMsg: 'something wrong'}`。 |
| onTap | EventHandle | 点击图片时触发。 |
| catchTap | EventHandle | 点击图片时触发，阻止事件冒泡。 |

注意：image 组件默认宽度 `300px`、高度 `225px`。

### mode

mode 有 14 种模式，包括 5 种缩放模式和 9 种裁剪模式。

#### 缩放模式

| 属性 | 描述 |
| --- | --- |
| scaleToFill | 不保持纵横比缩放，使图片的宽高完全拉伸至填满 image 元素 |
| aspectFit | 保持纵横比缩放，使图片的长边能完全显示出来。也就是说，可以完整地将图片显示出来 |
| aspectFill | 保持纵横比缩放，只保证图片的短边能完全显示出来。图片通常只在水平或垂直方向是完整的，另一个方向将会有所截取 |
| widthFix | 宽度不变，高度自动变化，保持原图宽高比不变 |
| heightFix | 高度不变，宽度自动变化，保持原图宽高比不变。版本要求：基础库 [2.7.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |

#### 裁剪模式

| 属性 | 描述 |
| --- | --- |
| top | 不缩放图片，只显示顶部区域 |
| bottom | 不缩放图片，只显示底部区域 |
| center | 不缩放图片，只显示中间区域 |
| left | 不缩放图片，只显示左边区域 |
| right | 不缩放图片，只显示右边区域 |
| top left | 不缩放图片，只显示左上边区域 |
| top right | 不缩放图片，只显示右上边区域 |
| bottom left | 不缩放图片，只显示左下边区域 |
| bottom right | 不缩放图片，只显示右下边区域 |

说明：图片高度不能设置为 `auto`，如果需要图片高度为 `auto`，直接设置 mode 为 `widthFix`。
## Bug & Tip

在 Android 系统中，如果给 `image` 设置缩放模式为 `mode="widthFix"` 的同时添加了 `display: flex` 样式，需要额外设置以下两种中的一种样式：

- 同时指定 `flex-direction: column`。
- 当 `flex-direction: row`（默认值）时，同时指定交叉轴对齐方式 `align-items`，并确保 `align-items` 不从 `normal`、`stretch`、`inherit`、`initial`、`unset` 中取值。

# 常见问题

### `image` 标签支持读取流文件吗？

小程序中显示二进制数据流的图片，需要先将二进制数据转成 base64 字符串，然后把 base64 字符串放在 `image` 中的 `src` 中实现显示。

### 为什么真机调用 `image` 组件，显示的图片被压缩？

建议把 `mode` 值设为 `widthFix`。

# 相关文档

- [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage)
- [my.compressImage](https://opendocs.alipay.com/mini/api/media/image/my.compressimage)
- [my.getImageInfo](https://opendocs.alipay.com/mini/api/media/image/my.getimageinfo)
- [my.previewImage](https://opendocs.alipay.com/mini/api/media/image/my.previewimage)
- [my.saveImage](https://opendocs.alipay.com/mini/api/media/image/my.saveimage)
