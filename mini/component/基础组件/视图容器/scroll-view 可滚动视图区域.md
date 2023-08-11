# 简介

可滚动视图区域。scroll-view 滚动条可以全局禁用滚动，但是无法禁用 scroll-view 中的滚动距离展示。

## 使用限制

- 使用竖向滚动时，需要指定固定高度，可通过 acss 设置 `height`。
- 在滚动 scroll-view 时会阻止页面回弹，所以在 scroll-view 中滚动，无法触发 `onPullDownRefresh` 下拉刷新功能。
- scroll-view 不支持 `scroll-x=true` 和 `scroll-y=true` 同时生效，只能用一个。可以使用 [view](/mini/component/view) 设置 `disable-scroll` 为 true 禁止滑动。
- scroll-view 满屏时，无法滑动页面，会导致导航栏滑动透明失效。可通过 [my.setNavigationBar](https://opendocs.alipay.com/mini/api/xwq8e6) 设置导航栏样式：导航栏标题、导航栏背景色、导航栏底部边框颜色、导航栏左上角 logo 图片。
- scroll-view 组件不支持自定义下拉刷新。
- scroll-view 组件的滚动条在 Android 中默认隐藏，仅在滑动时展示。在 iOS 中则无法隐藏。
- scroll-view 组件在 iOS 下不支持自定义修改，在 Android 下允许通过 `::-webkit-scrollbar` 自定义滚动条样式。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark/63eda77f-c032-4ede-937a-5f644305b10e/2018/jpeg/53e0ded7-1d92-45c7-8b5e-f0197c949767.jpeg#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/scroll-view/index&defaultOpenedFiles=pages/scroll-view/index&theme=light)

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| class | String | 外部样式名。 |
| style | String | 内联样式名。 |
| scroll-x | Boolean | 允许横向滚动。<br />**默认值：** false |
| scroll-y | Boolean | 允许纵向滚动。<br />**默认值：** false |
| upper-threshold | Number | 距顶部/左边多远时（单位 px），触发 `scrolltoupper` 事件。<br />**默认值：** 50 |
| lower-threshold | Number | 距底部/右边多远时（单位 px），触发 `scrolltolower` 事件。<br />**默认值：** 50 |
| scroll-top | Number | 设置竖向滚动条位置。 |
| scroll-left | Number | 设置横向滚动条位置。 |
| scroll-into-view | String | 滚动到子元素，值应为某子元素的 id。当滚动到该元素时，元素顶部对齐滚动区域顶部。<br />**说明：**`scroll-into-view` 的优先级高于 `scroll-top`。 |
| scroll-with-animation | Boolean | 在设置滚动条位置时使用动画过渡。<br />**默认值：** false |
| scroll-animation-duration | Number | 当 `scroll-with-animation`设置为 true 时，可以设置 `scroll-animation-duration` 来控制动画的执行时间，单位 ms。<br />**版本要求：** 基础库 [1.9.0](/mini/framework/compatibility) 及以上 |
| enable-back-to-top | Boolean | 当点击 iOS 顶部状态栏或者双击 Android 标题栏时，滚动条返回顶部，只支持竖向。<br />**默认值：** false<br />**版本要求：** 基础库 [1.11.0](/mini/framework/compatibility) 及以上 |
| trap-scroll | Boolean | 纵向滚动时，当滚动到顶部或底部时，强制禁止触发页面滚动，仍然只触发 scroll-view 自身的滚动。<br />**默认值：** false<br />**版本要求：** 基础库 [1.11.2](/mini/framework/compatibility) 及以上 |
| onScrollToUpper | EventHandle | 滚动到顶部/左边，会触发 `scrolltoupper` 事件。 |
| onScrollToLower | EventHandle | 滚动到底部/右边，会触发 `scrolltolower`事件。 |
| onScroll | EventHandle | 滚动时触发，`event.detail = {scrollLeft, scrollTop, scrollHeight, scrollWidth}`。 |
| onTouchStart | EventHandle | 触摸动作开始。<br />**版本要求：** 基础库 [1.15.0](/mini/framework/compatibility) 及以上 |
| onTouchMove | EventHandle | 触摸后移动。<br />**版本要求：** 基础库 [1.15.0](/mini/framework/compatibility) 及以上 |
| onTouchEnd | EventHandle | 触摸动作结束。<br />**版本要求：** 基础库 [1.15.0](/mini/framework/compatibility) 及以上 |
| onTouchCancel | EventHandle | 触摸动作被打断，如来电提醒、弹窗。<br />**版本要求：** 基础库 [1.15.0](/mini/framework/compatibility) 及以上 |
| disable-lower-scroll | String | 发生滚动前，对滚动方向进行判断，当方向是顶部/左边时，如果值为 `always` 将始终禁止滚动，如果值为 `out-of-bounds` 且当前已经滚动到顶部/左边，禁止滚动。<br />**版本要求**：基础库 [2.6.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| disable-upper-scroll | String | 发生滚动前，对滚动方向进行判断，当方向是底部/右边时，如果值为 `always` 将始终禁止滚动，如果值为 `out-of-bounds` 且当前已经滚动到底部/右边，禁止滚动。<br />**版本要求**：基础库 [2.6.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |

# FAQ

## 为何 scroll-view 在 popup 扩展组件中无法滑动？

popup 组件上加上 disableScroll={{false}} 属性才能滑动。

## 为何使用 swiper 嵌套 scroll-view，scroll-view 无法滑动？

swiper 和 scroll-view 均为滑动组件，如果必须使用，建议不做嵌套或者让 scroll-view 阻止 touch 事件冒泡即可：catchTouchStart、catchTouchMove。

## 如何监听 scroll-view 滚动到底部？

可以直接在 onScroll 方法中进行处理，使用 onScrollToLower 监听 scroll-view 的滚动高度来进行判断是否滑动到了底部。 scrollHeight 是 scroll-view 里面所有 view 的高度和，scrollTop 是滚动的值； scrollTop 的值等于 scrollHeight-scroll-view 视图的高度。

## 为何在页面有蒙层的情况下，外层滑动到底部，会导致蒙层也能滑动？

在外层 scroll-view 添加属性 trap-scroll。

## 为什么 onScrollToUpper 和 onScrollToLower 事件同时被触发，且触发了多次？

因为滚动时同时满足了距顶部 ${upper-threshold}px 内，距底部 ${lower-threshold}px 内，所以会同时触发 onScrollToUpper 和 onScrollToLower 事件。可以通过调整参数 upper-threshold 和 lower-threshold 避免一直处在触发区间来解决。

# 相关文档

- [view 视图容器](https://opendocs.alipay.com/mini/component/view)
- [my.setNavigationBar](https://opendocs.alipay.com/mini/api/xwq8e6)
- [popup 弹出菜单](https://opendocs.alipay.com/mini/component-ext/popup)
