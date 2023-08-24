# 简介

滑块视图容器。其中仅可放置 swiper-item，否则会导致未定义的行为。 swiper 的高度可以通过设置 swiper-item 元素高度来控制，也可以通过设置 swiper 的整体高度来控制（通过组件的 adjust-height 属性来具体实现）。

## 使用限制

- swiper 组件不可以放在地图上用，map 组件是由客户端创建的原生组件，原生组件的层级是最高的，所以页面中的其他组件无论设置 z-index 为多少，都无法在原生组件之上。
- swiper 组件的首张图片与左边的间隔可以和组件中 item 的图片间隔保持一致，可以根据 `previous-margin` 设置一下前边距。
- 调用 swiper 组件，swiper-item 嵌套 cover-view 会导致最后一个 swiper-item 后有很大的空白，且 swiper-item 不能添加事件，建议使用 [view](/mini/component/view) 做嵌套。
- swiper 可以有多个 swiper-item，默认只会展示一个滑块数量，可以通过传入 `display-multiple-items` 属性来修改数量限制。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark/b6227660-a40d-45a1-8b91-d76e5699d195/2018/jpeg/2b2fd77c-1145-4983-8f21-dd6a23e7d4ff.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/swiper/index&defaultOpenedFiles=pages/swiper/index&theme=light)

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| indicator-dots | Boolean | 是否显示指示点。<br />**默认值：** false |
| indicator-color | Color | 指示点颜色。<br />**默认值：** rgba(0, 0, 0, .3) |
| indicator-active-color | Color | 当前选中的指示点颜色。<br />**默认值：**#000 |
| active-class | String | `swiper-item` 可见时的 `class`。<br />**版本要求：** 基础库 [1.13.7](/mini/framework/compatibility) 以及上。 |
| changing-class | String | `acceleration` 设置为 `{{true}}` 时且处于滑动过程中，中间若干屏处于可见时的 `class`。<br />**版本要求：** 基础库 [1.13.7](/mini/framework/compatibility) 以及上。 |
| autoplay | Boolean | 是否自动切换。<br />**默认值：** false |
| current | Number | 当前页面的 index，可以增加左右箭头来控制轮播滚动。<br />**默认值：** 0 |
| duration | Number | 滑动动画时长。<br />**默认值：** 500(ms) |
| interval | Number | 自动切换时间间隔。<br />**默认值：** 5000(ms) |
| circular | Boolean | 是否启用无限滑动。<br />**默认值：** false |
| vertical | Boolean | 滑动方向是否为纵向。<br />**默认值：** false |
| previous-margin | String | 前边距，单位 px，1.9.0 暂时只支持水平方向。<br />**默认值：** 0px<br />**版本要求：** 基础库 [1.9.0](/mini/framework/compatibility) 及以上<br />**说明：** 去除 `previous-margin` 的设置距离可删除 swiper 组件左右空白距离。 |
| next-margin | String | 后边距，单位 px，1.9.0 暂时只支持水平方向。<br />**默认值：** 0px<br />**版本要求：** 基础库 [1.9.0](/mini/framework/compatibility) 及以上<br />**说明：** 去除 `next-margin` 的设置距离可删除 swiper 组件左右空白距离。 |
| acceleration | Boolean | 当开启时，会根据滑动速度，连续滑动多屏。<br />**默认值：** false<br />**版本要求：** 基础库 [1.13.7](/mini/framework/compatibility) 及以上 |
| disable-programmatic-animation | Boolean | 是否禁用代码变动触发 swiper 切换时使用动画。<br />**默认值：** false<br />**版本要求：** 基础库 [1.13.7](/mini/framework/compatibility) 及以上 |
| onChange | EventHandle | current 改变时会触发，`event.detail = {current, isChanging}`，其中 `isChanging` 需 `acceleration` 设置为 `{{true}}` 时才有值，当连续滑动多屏时，中间若干屏触发 `onChange` 事件时 `isChanging` 为 `true`，最后一屏返回 `false`。<br />**版本要求：** 基础库 [1.15.0](/mini/framework/compatibility) 及以上 |
| onTransition | EventHandle | swiper 中 swiper-item 的位置发生改变时会触发 transition 事件。<br />其中{dx,dy} = event.detail 基础库 [2.6.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。 |
| onAnimationEnd | EventHandle | 动画结束时会触发 animationEnd 事件，`event.detail = {current, source}`，其中 `source` 的值有 `autoplay` 和 `touch`。<br />**版本要求：** 基础库 [1.15.0](/mini/framework/compatibility) 及以上 |
| disable-touch | Boolean | 是否禁止用户 touch 操作。<br />**默认值：** false<br />**版本要求：** 基础库 [1.15.0](/mini/framework/compatibility) 及以上 |
| swipe-ratio | Number | 滑动距离阈值，当滑动距离超过阈值时进行 swiper-item 切换。<br />**默认值**：0.2<br />**版本要求**：基础库 [1.24.11](/mini/framework/compatibility) 及以上 |
| swipe-speed | Number | 滑动综合速度阈值，当超过阈值时进行 swiper-item 切换，数值越小越敏感。<br />**默认值**：0.05<br />**版本要求**：基础库 [1.24.11](/mini/framework/compatibility) 及以上 |
| touch-angle | Number | 计算用户手势时所依赖的滑动角度。角度根据 touchstart 事件和首次 touchmove 事件的坐标计算得出。数值越小越对用户的滑动方向准确度要求越高。<br />**默认值**：45<br />**版本要求**：基础库 [1.24.11](/mini/framework/compatibility) 及以上 |
| display-multiple-items | Number | 同时显示的滑块数量。<br />**默认值**：1<br />**版本要求**：基础库 [2.6.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上|
| easing-function | String | 切换缓动动画类型。<br />**默认值**：default<br />**版本要求**：基础库 [2.6.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上。属性值有`default`、`linear`、`easeInCubic`、`easeOutCubic`、`easeInOutCubic` |
| snap-to-edge | Boolean | 当 swiper-item 个数大于等于 2，关闭 circular 并且开启 previous-margin 或 next-margin 时，可以指定这个边距是否应用到第一个、最后一个元素。<br />**默认值**：false<br />**版本要求**：基础库 [2.6.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| adjust-height | String | 自动以指定滑块的高度为整个容器的高度。当 vertical 为 true 时，默认不调整。可选值为：<br /><ul><li>first：第一个滑块。</li><li>current：实时的当前滑块。</li><li>highest：高度最大的滑块。</li><li>none：不根据滑块调整高度，容器高度取决于自身样式。</li></ul> **默认值**：first<br />**版本要求**：基础库 [2.6.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| adjust-vertical-height | Boolean | vertical 为 true 时强制使 adjust-height 生效。<br />**默认值**：false<br />**版本要求**：基础库 [2.6.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
