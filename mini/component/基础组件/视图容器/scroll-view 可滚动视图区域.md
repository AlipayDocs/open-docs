# 简介

可滚动视图区域。`scroll-view` 的滚动条可以通过全局设置禁用滚动，但无法禁用 `scroll-view` 中的滚动距离展示。

## 使用限制

- 使用竖向滚动时，需要给定固定高度，可以通过 acss 设置 `height`。
- 在滚动 `scroll-view` 时会阻止页面回弹，因此 `scroll-view` 中的滚动无法触发 `onPullDownRefresh` 下拉刷新功能。
- `scroll-view` 不支持 `scroll-x=true` 和 `scroll-y=true` 同时生效；只能选择其一。可以通过 [view](/mini/component/view) 设置 `disable-scroll=true` 禁止滑动。
- 当 `scroll-view` 占满屏幕时，页面无法滚动，可能会造成导航栏滑动透明度失效。可以用 [my.setNavigationBar](https://opendocs.alipay.com/mini/api/xwq8e6) 方法设置导航栏样式，包括标题、背景色、底部边框颜色以及左上角 logo 图片等。
- `scroll-view` 组件不支持自定义下拉刷新功能。
- `scroll-view` 的滚动条在 Android 中默认为隐藏状态，仅在滑动时才会显示出来。而在 iOS 中，滚动条是无法隐藏的。
- `scroll-view` 组件在 iOS 上不能自定义滚动条样式；在 Android 上，可以使用 `::-webkit-scrollbar` 自定义滚动条样式。

## 扫码体验

![二维码](https://gw.alipayobjects.com/zos/skylark/63eda77f-c032-4ede-937a-5f644305b10e/2018/jpeg/53e0ded7-1d92-45c7-8b5e-f0197c949767.jpeg)
# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/scroll-view/index&defaultOpenedFiles=pages/scroll-view/index&theme=light)

## 属性说明

> 表格中 “-” 代表支持。

| 属性 | 类型 | 描述 | WebView 兼容性 | Native 兼容性 |
| --- | --- | --- | --- | --- |
| class | String | 外部样式名 | - | - |
| style | String | 内联样式名 | - | - |
| scroll-x | Boolean | 允许横向滚动。<br />**默认值：** false | - | - |
| scroll-y | Boolean | 允许纵向滚动。<br />**默认值：** false | - | - |
| upper-threshold | Number | 距顶部/左边多远时（单位 px），触发 `scrolltoupper` 事件。<br />**默认值：** 50 | - | - |
| lower-threshold | Number | 距底部/右边多远时（单位 px），触发 `scrolltolower` 事件。<br />**默认值：** 50 | - | - |
| scroll-top | Number | 设置竖向滚动条位置 | - | - |
| scroll-left | Number | 设置横向滚动条位置 | - | - |
| scroll-into-view | String | 滚动到子元素，值应为某子元素的 id。当滚动到该元素时，元素顶部对齐滚动区域顶部。<br />**说明：** `scroll-into-view` 的优先级高于 `scroll-top` | - | 暂不支持 |
| scroll-with-animation | Boolean | 在设置滚动条位置时使用动画过渡。<br />**默认值：** false | - | - |
| scroll-animation-duration | Number | 当 `scroll-with-animation` 设置为真时，可以设置 `scroll-animation-duration` 来控制动画的执行时间，单位毫秒 | 基础库 1.9.0+ | - |
| enable-back-to-top | Boolean | 当点击 iOS 顶部状态栏或者双击 Android 标题栏时，滚动条返回顶部，只支持竖向。<br />**默认值：** false | 基础库 1.11.0+ | - |
| trap-scroll | Boolean | 纵向滚动时，当滚动到顶部或底部时，强制禁止触发页面滚动，仍然只触发 scroll-view 自身的滚动。<br />**默认值：** false | 基础库 1.11.2+ | - |
| onScrollToUpper | EventHandle | 滚动到顶部/左边，会触发 `scrolltoupper` 事件 | - | - |
| onScrollToLower | EventHandle | 滚动到底部/右边，会触发 `scrolltolower` 事件 | - | - |
| onScroll | EventHandle | 滚动时触发，`event.detail = {scrollLeft, scrollTop, scrollHeight, scrollWidth}` | - | - |
| onTouchStart | EventHandle | 触摸动作开始 | 基础库 1.15.0+ | - |
| onTouchMove | EventHandle | 触摸后移动 | 基础库 1.15.0+ | - |
| onTouchEnd | EventHandle | 触摸动作结束 | 基础库 1.15.0+ | - |
| onTouchCancel | EventHandle | 触摸动作被打断，如来电提醒、弹窗 | 基础库 1.15.0+ | - |
| disable-lower-scroll | String | 发生滚动前，对滚动方向进行判断，当方向是顶部/左边时，如果值为 `always` 将始终禁止滚动，如果值为 `out-of-bounds` 且当前已经滚动到顶部/左边，禁止滚动 | 基础库 2.6.2+ | - |
| disable-upper-scroll | String | 发生滚动前，对滚动方向进行判断，当方向是底部/右边时，如果值为 `always` 将始终禁止滚动，如果值为 `out-of-bounds` 且当前已经滚动到底部/右边，禁止滚动 | 基础库 2.6.2+ | - |

上表的修改针对以下方面：
- 删除无关的空格和换行，使内容紧凑、干净。
- 修正了一些标点使用上的不规范，比如属性描述中不使用句号。
- 移除了没必要的粗体标记，以符合表格内容的规范。
- 调整引用链接的格式，遵循 Markdown 链接语法规范。
# FAQ

## 为什么 scroll-view 在 popup 扩展组件中不能滑动？

在 popup 组件上添加 `disableScroll={{false}}` 属性，才能实现滑动。

## 为什么当 scroll-view 嵌入到 swiper 中时，无法滑动？

因为 swiper 和 scroll-view 都是滑动组件。如果必须要同时使用它们，建议不要将 scroll-view 嵌套在 swiper 中，或者设置 scroll-view 来阻止触摸事件的冒泡，比如使用 `catchTouchStart`、`catchTouchMove`。

## 如何判断 scroll-view 是否滚动到底部？

你可以在 `onScroll` 方法中处理这个问题，或者使用 `onScrollToLower` 监听 `scroll-view` 的滚动高度，来判断是否已经滑动到底部。`scrollHeight` 是 `scroll-view` 内部所有视图的总高度，`scrollTop` 是当前滚动的高度；当 `scrollTop` 的值等于 `scrollHeight` 减去 `scroll-view` 视图高度时，就表示滚动到了底部。

## 为什么在页面上有蒙层时，外层滑动到底部会导致蒙层也能滑动？

你应在外层的 `scroll-view` 上添加 `trap-scroll` 属性来解决这个问题。

## 为什么 `onScrollToUpper` 和 `onScrollToLower` 事件会被同时触发，并且触发多次？

这是因为滚动行为同时满足了距顶部 `upper-threshold` 内和距底部 `lower-threshold` 内的条件，导致 `onScrollToUpper` 和 `onScrollToLower` 事件都被触发。为了避免频繁触发，可以通过调整 `upper-threshold` 和 `lower-threshold` 的值，避免一直处于触发区域。

# 相关文档

- [view 视图容器](https://opendocs.alipay.com/mini/component/view)
- [my.setNavigationBar](https://opendocs.alipay.com/mini/api/xwq8e6)
- [popup 弹出菜单](https://opendocs.alipay.com/mini/component-ext/popup)
