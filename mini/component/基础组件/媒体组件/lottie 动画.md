# 简介

Lottie 是一个用于 Web 和 iOS、Android 的移动库，可使用 Bodymovin 解析以 JSON 格式导出的 Adobe After Effects 动画，并将其本地呈现在移动设备上。以下为 Lottie 动画库适配小程序的方法。有关 Lottie 的详情可查看 [Lottie 官方文档](https://github.com/airbnb/lottie-web) 和 [Lottie 官方支持能力列表](http://airbnb.io/lottie/#/supported-features)。相关 API 详情可查看 [my.createLottieContext](https://opendocs.alipay.com/mini/api/createlottiecontext)。

## 使用限制

支付宝 10.1.35 版本及以上支持 Lottie 动画。

# 使用

## 示例代码

### .axml 示例代码

```html
<!--.axml-->
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
// .js
// .js 
Page({
	data: {
		item: {
			id: 'lottie-1',
			desc: 'Django自动播放,低端设备降级',
			autoplay: true,
			path:'https://private-alipayobjects.alipay.com/alipay-rmsdeploy-image/rmsportal/ccVuojvUKLkFENNHAVgT.json',
			placeholder:'https://gw.alipayobjects.com/mdn/rms_e345fe/afts/img/A*nu3GTaHqJ9AAAAAAAAAAAAAAARQnAQ524560995883_icon_S.png',
			optimize: 'true',
			repeatCount: -1,  
      assetsPath : 'https://gw.alipayobjects.com/os/lottie-asset/bb/data.json/'
		} 
	},
  	onReady() {
    	var lottieContext = my.createLottieContext(this.data.item.id);
		lottieContext.play()
    }
})
```

### .acss 示例代码

```css
/*.acss*/
.item {
  width: 700rpx;
  height: 400rpx;
  /* opacity: 0.5; */
}
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| autoplay | Boolean | false | 是否自动播放。<br />**默认值：** false |
| path | String | false | Lottie 资源地址。包含近端（包内地址）和远端（网络）的 JSON 文件地址。 |
| speed | Float | false | 播放速度。正数为正向播放，负数负向播放。<br />**默认值：** 1.0 |
| repeat-count | Number | false | 循环次数。 <br /><ul><li>如果是负数表示无限次。</li><li>如果是 0 表示不循环，播放一次。</li><li>如果是 1 表示循环一次，播放两次。</li></ul> **默认值：** 0<br />**版本要求：** 支付宝客户端 10.1.80 及以上 |
| auto-reverse | Boolean | false | 是否自动回播。<br />**默认值：** false |
| assets-path | String | false | 资源地址。"/" 表明是小程序根目录。<br />**版本要求：** 支付宝客户端 10.1.50 及以上 |
| placeholder | String | true | 兜底图或者降级图地址。<br /><ul><li>1. 支持本地资源，案例：'/image/lottie/lottie2_default.png'。</li><li>支持 http 的 cdn 地址、近端地址。</li></ul> **版本要求：** 支付宝客户端 10.1.52 及以上 ||
| md5 | String | false | 在线资源的 md5 校验。<br />可以使用 b.zip 加密 获取 md5 值<br />md5="77c6c86fc89ba94cc0a9271b77ae77d2"<br />**版本要求：** 支付宝客户端 10.1.52 及以上 |
| optimize | Boolean | false | 降级。降级是指如遇低端设备，Lottie 会降级展示为 placeholder。<br />当 optimize 为 true ，并且传入了 placeholder 时，在低端设备上只会展示 placeholder，不展示 Lottie。<br />低端设备如下所示：<br /><ul><li>iOS ：小于等于 iPhone6P</li><li>Android：内存容量小于 3G</li></ul> **默认值：** false<br />**版本要求：** 支付宝客户端 10.1.52 及以上 |
| onDataReady | EventHandle | - | 当数据下载+视图创建完成时触发。 |
| onDataFailed | EventHandle | - | 数据加载失败时触发。 |
| onAnimationStart | EventHandle | - | 动画开始时触发。 |
| onAnimationEnd | EventHandle | - | 动画结束时触发。 |
| onAnimationRepeat | EventHandle | - | 动画一次重播结束。<br />**版本要求**：支付宝客户端 10.1.52 及以上 |
| onAnimationCancel | EventHandle | - | 动画取消。业务调用 Cancel 时回调。 |
| onDataLoadReady | EventHandle | - | 参数化时，数据准备完成，等待业务传入参数化值。<br />**版本要求**：支付宝客户端 10.1.72 及以上 |

## 功能介绍

支付宝小程序接入 Lottie 支持如下功能：

- 资源文件处理：Lottie 内如何处理图片、资源。
- 播放能力：如何在没有控制层的前提下有自定义播放能力。

### 资源文件处理 ﻿

#### 图片文件

UI 设计师提供的 Lottie 动画可能会带有目录 `images/`，里面保存的是一些静态图片。 <br />目前有三种解决方案，推荐前两种：

1. 整体压缩为 Zip 文件，将 Zip 的路径放在 path 参数里。
1. 将图片资源转成 base64 内链在 JSON 文件里，这样 JSON 路径放在 path 参数里。
1. 如果图片资源和 JSON 文件是分离的，那么需要以下处理：动画描述的 .json 文件里，对图片资源是这样定位的：

```json
{ "id": "image_0", "w": 66, "h": 89, "u": "images/", "p": "img_0.png" }
```

- w：宽度
- h：高度
- u：根目录
- p：具体文件<br />因此如果图片资源统一放在一个单独 URL 里，例如 `http://xxx.xxx.com/images/img_0.png`，那么需要将 `http://xxx.xxx.com/` 配置在 `assetsPath` 参数中。

#### Base64 support

Lottie 对资源的定义是

```json
{ "id": "image_0", "w": 66, "h": 89, "u": "images/", "p": "img_0.png" }
```

10.1.52 版本开始，p 节点支持 base64，当使用 base64 时，可以忽略 u 节点，例如：

```json
"p":"data:image/png;base64,iVBORw0KGgoAAAANSU...."
```

**注意：** 如果在支付宝 10.1.52、10.1.60 版本中使用 Base64 资源，需要在 JSON 文件中增加 assetsPath="/" 作为参数，否则 iOS 上可能无法显示。

# 常见问题

## 修复兼容性问题

如果提示“使用插件版本 5.5.0+，客户端必须也是 5.5.0+，iOS/android 旧版播放器会闪退”，必须重新用兼容性模式导出 JSON。

## 真机测试

请尽量分别使用不同系统下的不同机型进行测试，提高正确性。

### 选用兼容版本

支付宝版本为 10.1.68 或更低版本时，如果有 iOS 播放不完整、或者 Android 播放闪退的情况，请 UI 设计师使用 AE 插件导出时选用兼容版本。 **说明：**

- Lottie 在 Android 7.0 上硬件加速的问题请参见官方 issue：[https://github.com/airbnb/lottie-android/issues/1453](https://github.com/airbnb/lottie-android/issues/1453)；
- 客户端 10.1.82 版本默认对 Android7.0 使用软件渲染的方式。

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386206315-1a7b0a9a-2c86-47c3-b73d-5b646c932d7f.png)

### 检查字体问题

支付宝版本 10.1.72 以下如果用到了 JSON 里面有 font-family="PingFang SC" 的字体，请检查字体问题。因为 Android 没有这个字体，在 Android 某些机器上（以下为部分闪退机型列表）会闪退。

| MI 8       |
| ---------- |
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

如果已经加载了 Lottie 动画，可选择在开发者选项里面关闭动画，关闭后需要重启 App 或者重新加载才可以恢复 Lottie。

## 应用切回前台需重新添加动画

iOS 系统在应用切到后台的时候会自动移除动画，在应用切回前台时需要重新添加动画。

## 保证小程序组件 ID 应用内唯一

小程序组件 ID 需应用内保证唯一。不同的 Page 的同一个 Lottie 组件，页面切换后组件未必会销毁，因此不建议复用，例如：可翻页的视频页面中的点赞按钮。

## 文件压缩

请在文件当前目录直接进行压缩，不要在外层目录进行压缩。当前不支持遍历目录寻找 JSON 文件，如果解压后第一层未发现 JSON 文件则会被认为不合法。

![](https://cdn.nlark.com/yuque/0/2022/png/179989/1649386210607-94810890-adb0-43d3-9306-47f9c98c4afc.png)

支持本地 json 文件的解决办法：

```json
//mini.project.json
{
"enableAppxNg"：true,
"miniprogramRoot"："dist",
"scripts"：{
  "beforePreview"："tnpm run build",
  "beforeUpload"："tnpm run build"
 }
"include"：["**/*.json"] //添加这行
}
```
