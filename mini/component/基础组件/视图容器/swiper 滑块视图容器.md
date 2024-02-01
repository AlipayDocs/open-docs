# 简介

滑块视图容器。其中仅可放置 `swiper-item` 组件，否则会导致未定义的行为。`swiper` 的高度可以通过设置 `swiper-item` 元素的高度来控制，也可以通过设置 `swiper` 的整体高度来控制（通过组件的 `adjust-height` 属性来具体实现）。

## 使用限制

- `swiper` 组件不可以放在地图上用，`map` 组件是由客户端创建的原生组件，原生组件的层级是最高的。所以，页面中的其他组件无论设置 `z-index` 为多少，都无法覆盖原生组件。
- `swiper` 组件的首张图片与左侧间隔可与组件中的其他图片间隔保持一致。间隔可通过 `previous-margin` 属性设定。
- 使用 `swiper` 组件时，若 `swiper-item` 嵌套 `cover-view`，可能会导致最后一个 `swiper-item` 后面出现很大的空白。且 `swiper-item` 不能添加事件处理，建议使用 [view](/mini/component/view) 组件进行嵌套。
- `swiper` 可以包含多个 `swiper-item`，但同时在前台完整展示的只能有一个。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark/b6227660-a40d-45a1-8b91-d76e5699d195/2018/jpeg/2b2fd77c-1145-4983-8f21-dd6a23e7d4ff.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)
# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/swiper/index&defaultOpenedFiles=pages/swiper/index&theme=light)

## 属性说明

> 表格中的 "—" 代表该属性被支持。

| 属性                   | 类型    | 描述                                                               | WebView 兼容性                                                           | Native 兼容性                                        |
| ---------------------- | ------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------- | ---------------------------------------------------- |
| indicator-dots         | Boolean | 是否显示指示点。<br />**默认值：** false                             | —                                                                         | —                                                    |
| indicator-color        | Color   | 指示点颜色。<br />**默认值：** rgba(0, 0, 0, .3)                     | —                                                                         | —                                                    |
| indicator-active-color | Color   | 当前选中的指示点颜色。<br />**默认值：** #000                         | —                                                                         | —                                                    |
| active-class           | String  | `swiper-item` 可见时的 `class`。                                     | 基础库 [1.13.7+](/mini/framework/compatibility)                          | —                                                    |
| changing-class         | String  | `acceleration` 设置为 `true` 时，滑动过程中可见的 `class`。         | 基础库 [1.13.7+](/mini/framework/compatibility)                          | —                                                    |
| autoplay               | Boolean | 是否自动切换。<br />**默认值：** false                                  | —                                                                         | —                                                    |
| current                | Number  | 当前页面的索引，可以通过左右箭头控制滑动。<br />**默认值：** 0        | —                                                                         | —                                                    |
| duration               | Number  | 滑动动画时长，单位为 ms。<br />**默认值：** 500                       | —                                                                         | —                                                    |
| interval               | Number  | 自动切换的时间间隔，单位为 ms。<br />**默认值：** 5000                | —                                                                         | —                                                    |
| circular               | Boolean | 是否启用无限滑动。<br />**默认值：** false                              | —                                                                         | —                                                    |
| vertical               | Boolean | 滑动方向是否为纵向。<br />**默认值：** false                            | —                                                                         | —                                                    |
| previous-margin        | String  | 前面的边距，单位为 px。<br />**默认值：** 0px<br />**说明：** 移除 `previous-margin` 可删除 swiper 组件的左右空白。  | 基础库 [1.9.0+](/mini/framework/compatibility)                           | 基础库 [2.9.7+](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)，Android 不支持 |
| next-margin            | String  | 后面的边距，单位为 px。<br />**默认值：** 0px<br />**说明：** 移除 `next-margin` 可删除 swiper 组件的左右空白。        | 基础库 [1.9.0+](/mini/framework/compatibility)                           | 基础库 [2.9.7+](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)，Android 不支持 |
| acceleration           | Boolean | 开启时，根据滑动速度滑动多屏。<br />**默认值：** false                  | 基础库 [1.13.7+](/mini/framework/compatibility)                          | —                                                    |
| disable-programmatic-animation | Boolean | 禁用代码变动触发的 swiper 切换动画。<br />**默认值：** false        | 基础库 [1.13.7+](/mini/framework/compatibility)                          | —                                                    |
| onChange               | EventHandle | current 改变时触发，`event.detail = {current, isChanging}`。<br />`isChanging` 值在 `acceleration` 为 `true` 时有效。| 基础库 [1.15.0+](/mini/framework/compatibility)                          | —                                                    |
| onTransition           | EventHandle | swiper 中 swiper-item 位置改变时触发，`{dx, dy} = event.detail`。 | 基础库 [2.6.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) | 不支持                                               |
| onAnimationEnd         | EventHandle | 动画结束时触发，`event.detail = {current, source}`。<br />`source` 的值有 `autoplay` 或 `touch`。  | 基础库 [1.15.0+](/mini/framework/compatibility)                          | 不支持                                               |
| disable-touch          | Boolean | 是否禁止用户触摸操作。<br />**默认值：** false                          | 基础库 [1.15.0+](/mini/framework/compatibility)                          | —                                                    |
| swipe-ratio            | Number  | 滑动距离阈值，超过阈值时切换 swiper-item。<br />**默认值：** 0.2       | 基础库 [1.24.11+](/mini/framework/compatibility)                         | —                                                    |
| swipe-speed            | Number  | 滑动速度阈值，超过阈值时切换 swiper-item，数值越小越敏感。<br />**默认值：** 0.05 | 基础库 [1.24.11+](/mini/framework/compatibility)                         | —                                                    |
| touch-angle            | Number  | 滑动角度阈值，用于计算用户手势，数值越小要求越高。<br />**默认值：** 45 | 基础库 [1.24.11+](/mini/framework/compatibility)                         | —                                                    |
| display-multiple-items | Number  | 同时显示的滑块数量。<br />**默认值：** 1                                | 基础库 [2.6.4+](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) | —                                                    |
| easing-function        | String  | 切换缓动动画类型。<br />**默认值：** default<br />可选值有 `default`、`linear`、`easeInCubic`、`easeOutCubic`、`easeInOutCubic`  | 基础库 [2.6.4+](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) | —                                                    |
| snap-to-edge           | Boolean | 当 swiper-item 数量大于等于 2，关闭 circular 同时开启 previous-margin 或 next-margin 时，是否应用边距到第一个或最后一个元素。<br />**默认值：** false | 基础库 [2.6.4+](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) | —                                                    |
| adjust-height          | String  | 调整 swiper 高度为指定滑块的高度，可选值：<br />`first`：第一个滑块。<br />`current`：当前滑块。<br />`highest`：最高滑块。<br />`none`：自定义高度。<br />**默认值：** first | 基础库 [2.6.4+](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) | —                                                    |
| adjust-vertical-height | Boolean | 是否调整 vertical 为 true 时的 swiper 高度。<br />**默认值：** false    | 基础库 [2.6.4+](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) | —                                                    |
