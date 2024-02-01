# 简介

Lottie 是一个适用于 Web 与 iOS、Android 的移动库。该库能够使用 Bodymovin 解析 Adobe After Effects 导出的 JSON 格式动画，并能够在移动设备上本地呈现。以下为 Lottie 动画库适配小程序的方法。有关 Lottie 的更多信息，可以查阅 [Lottie 官方文档](https://github.com/airbnb/lottie-web) 和 [Lottie 官方支持能力列表](http://airbnb.io/lottie/#/supported-features)。详细的 API 信息可以参阅 [my.createLottieContext](https://opendocs.alipay.com/mini/api/createlottiecontext)。

## 使用限制

支付宝版本 10.1.35 及以上支持 Lottie 动画。
# 使用

## 示例代码

### .axml 示例代码

```html
<!-- .axml 文件 -->
<lottie
  assets-path="{{item.assetsPath}}"
  autoplay="{{item.autoplay}}"
  id="{{item.id}}"
  path="{{item.path}}"
  repeat-count="{{item.repeatCount}}"
  placeholder="{{item.placeholder}}"
  class="item">
</lottie>
```

### .js 示例代码

```javascript
// .js 文件
Page({
  data: {
    item: {
      id: 'lottie-1',
      desc: '使用 Django 自动播放，对低端设备进行降级处理',
      autoplay: true,
      path: 'https://private-alipayobjects.alipay.com/alipay-rmsdeploy-image/rmsportal/ccVuojvUKLkFENNHAVgT.json',
      placeholder: 'https://gw.alipayobjects.com/mdn/rms_e345fe/afts/img/A*nu3GTaHqJ9AAAAAAAAAAAAAAARQnAQ524560995883_icon_S.png',
      optimize: 'true',
      repeatCount: -1,
      assetsPath: 'https://gw.alipayobjects.com/os/lottie-asset/bb/data.json/'
    }
  },
  onReady() {
    var lottieContext = my.createLottieContext(this.data.item.id);
    lottieContext.play();
  }
});
```
### .acss 示例代码

```css
/* .acss */
.item {
  width: 700rpx;
  height: 400rpx;
  /* opacity: 0.5; */
}
```

## 属性说明

| 属性         | 类型    | 必填  | 描述                                             |
| ------------ | ------- | ----- | ------------------------------------------------ |
| autoplay     | Boolean | false | 是否自动播放。默认值：false                      |
| path         | String  | false | Lottie 资源地址，包含近端和远端的 JSON 文件地址。 |
| speed        | Float   | false | 播放速度，正数正向播放，负数负向播放。默认值：1.0 |
| repeat-count | Number  | false | 循环次数。负数表示无限次，0 表示不循环，1 表示循环一次。默认值：0。支付宝客户端 10.1.80 及以上版本支持。 |
| auto-reverse | Boolean | false | 是否自动回播。默认值：false                      |
| assets-path  | String  | false | 资源地址，“/” 表示小程序根目录。支付宝客户端 10.1.50 及以上版本支持。 |
| placeholder  | String  | true  | 兜底图或降级图地址，支持本地资源和 http cdn 地址。支付宝客户端 10.1.52 及以上版本支持。 |
| md5          | String  | false | 在线资源的 md5 校验值。支付宝客户端 10.1.52 及以上版本支持。 |
| optimize     | Boolean | false | 当 optimize 为 true 时，在低端设备上只会展示 placeholder，不展示 Lottie。默认值：false。支付宝客户端 10.1.52 及以上版本支持。 |
| onDataReady  | EventHandle | -   | 当数据下载和视图创建完成时触发。                    |
| onDataFailed | EventHandle | -   | 数据加载失败时触发。                              |
| onAnimationStart | EventHandle | - | 动画开始时触发。                                |
| onAnimationEnd | EventHandle | - | 动画结束时触发。                                |
| onAnimationRepeat | EventHandle | - | 动画一次重播结束。支付宝客户端 10.1.52 及以上版本支持。 |
| onAnimationCancel | EventHandle | - | 动画取消，业务调用 Cancel 时回调。               |
| onDataLoadReady | EventHandle | - | 参数化时，数据准备完成，等待业务传入参数化值。支付宝客户端 10.1.72 及以上版本支持。 |
## 功能介绍

支付宝小程序接入 Lottie 支持以下功能：

- 资源文件处理：Lottie 中图片、资源的处理方式。
- 播放能力：无控制层的情况下，如何自定义播放能力。

### 资源文件处理

#### 图片文件

UI 设计师提供的 Lottie 动画可能会包含 `images/` 目录，其中保存了一些静态图片。目前有三种解决方案，推荐前两种：

1. 将整体压缩成 Zip 包，并将路径配置在 `path` 参数中。
2. 将图片资源转换成 Base64 编码，并内联于 JSON 文件中，然后将 JSON 路径配置在 `path` 参数中。
3. 如果图片资源与 JSON 文件分离，那么需要进行以下处理：动画描述的 `.json` 文件中，对图片资源的定位如下：

```json
{ "id": "image_0", "w": 66, "h": 89, "u": "images/", "p": "img_0.png" }
```

- `w`：宽度
- `h`：高度
- `u`：根目录
- `p`：具体文件

因此，如果图片资源统一放在一个单独的 URL 中，比如 `http://xxx.xxx.com/images/img_0.png`，则需要将 `http://xxx.xxx.com/` 配置在 `assetsPath` 参数中。

#### Base64 支持

Lottie 对资源的定义是：

```json
{ "id": "image_0", "w": 66, "h": 89, "u": "images/", "p": "img_0.png" }
```

从 10.1.52 版本开始，`p` 节点支持 Base64 编码。当使用 Base64 时，可以忽略 `u` 节点，例如：

```json
"p":"data:image/png;base64,iVBORw0KGgoAAAANSU...."
```

**注意：** 如果在支付宝 10.1.52 或 10.1.60 版本中使用 Base64 资源，需要在 JSON 文件中增加 `assetsPath="/"` 作为参数，否则在 iOS 设备上可能无法显示。
# 常见问题

## 修复兼容性问题

如果提示“使用插件版本 5.5.0+，客户端必须也是 5.5.0+，iOS/android 旧版播放器会闪退”，必须重新用兼容性模式导出 JSON。

## 真机测试

请尽量分别使用不同系统下的不同机型进行测试，以提高准确性。

### 选用兼容版本

当支付宝版本为 10.1.68 或更低版本时，如果在 iOS 上播放不完整，或在 Android 上播放时闪退，请 UI 设计师在使用 AE 插件导出时选用兼容版本。**说明：**

- Lottie 在 Android 7.0 上硬件加速的问题，请参见官方 issue：[https://github.com/airbnb/lottie-android/issues/1453](https://github.com/airbnb/lottie-android/issues/1453)。
- 客户端 10.1.82 版本默认对 Android 7.0 使用软件渲染的方式。

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386206315-1a7b0a9a-2c86-47c3-b73d-5b646c932d7f.png)

### 检查字体问题

当支付宝版本为 10.1.72 以下，并且 JSON 中使用了 font-family="PingFang SC" 的字体时，请检查字体问题。由于 Android 不含该字体，在以下部分机型上可能导致闪退。

| 机型       |
| ---------- |
| MI 8       |
| EML-AL00   |
| OPPO R11   |
| vivo Y66L  |
| MIX 3      |
| vivo NEX A |
| VOG-AL10   |
| PBET00     |
| V1829A     |
| vivo X20A  |

## 开发者选项中关闭动画

如果已经加载了 Lottie 动画，你可以在开发者选项里关闭动画。关闭之后，你需要重启 App 或重新加载页面才可恢复 Lottie 动画。

## 应用切回前台需重新添加动画

iOS 系统在应用切换到后台时会自动移除动画。当应用切回前台时，需要重新添加动画。
## 保证小程序组件 ID 应用内唯一

小程序组件 ID 必须在应用内保持唯一。如果不同页面含有相同的 Lottie 组件，在页面切换后，组件可能不会销毁。因此，建议避免复用相同的组件 ID，例如：可翻页的视频页面中的点赞按钮。

## 文件压缩

请在文件所在的当前目录进行压缩，不要在该目录的外层进行压缩。系统当前不支持遍历目录查找 JSON 文件。如果解压后的第一层目录中未发现 JSON 文件，该目录会被认为是不合法的。

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386210607-94810890-adb0-43d3-9306-47f9c98c4afc.png)

支持本地 JSON 文件的解决方法：

```json
// mini.project.json
{
  "enableAppxNg": true,
  "miniprogramRoot": "dist",
  "scripts": {
    "beforePreview": "tnpm run build",
    "beforeUpload": "tnpm run build"
  },
  "include": ["**/*.json"] // 添加这行
}
```
