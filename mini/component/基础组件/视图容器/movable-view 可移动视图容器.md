# 简介

可移动的视图容器，在页面中可以拖拽滑动。`movable-view` 必须在 [movable-area](https://opendocs.alipay.com/mini/component/movable-area) 组件中，并且必须是直接子节点，否则不能移动。

## 使用限制

- 版本要求基础库 1.11.0 及以上；若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('movable-view')` 判断是否支持。
- `movable-view` 必须设置 `width` 和 `height` 属性，否则默认为 `10px`。
- `movable-view` 默认为绝对定位，请不要修改其属性；`top` 和 `left` 属性默认为 `0px`。
- 当 `movable-view` 小于 [movable-area](https://opendocs.alipay.com/mini/component/movable-area) 时，`movable-view` 的移动范围在 `movable-area` 内。当 `movable-view` 大于 `movable-area` 时，`movable-view` 的移动范围必须包含 `movable-area`（`x` 轴方向和 `y` 轴方向分开考虑）。

## 扫码体验

![](https://gw.alipayobjects.com/mdn/rms_d929c6/afts/img/A*V9IxRbitTwkAAAAAAAAAAABjARQnAQ#align=left&display=inline&height=158&originHeight=1906&originWidth=1540&status=done&width=128)
# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/movable-view/index&defaultOpenedFiles=pages/movable-view/index&theme=light)

## 属性说明

| 属性              | 类型     | 描述                                                                                       |
| ----------------- | -------- | ------------------------------------------------------------------------------------------ |
| direction         | String   | `movable-view` 的移动方向，属性值有 `all`、`vertical`、`horizontal`、`none`。<br />默认值：none |
| inertia           | Boolean  | `movable-view` 是否带有惯性。<br />默认值：false<br />版本要求：基础库 1.20.0 及以上          |
| out-of-bounds     | Boolean  | 超过可移动区域后，`movable-view` 是否还可以移动。<br />默认值：false<br />版本要求：基础库 1.20.0 及以上   |
| x                 | Number   | 定义 x 轴方向的偏移，会换算为 left 属性，如果 x 的值不在可移动范围内，会自动移动到可移动范围。<br />默认值：0 |
| y                 | Number   | 定义 y 轴方向的偏移，会换算为 top 属性，如果 y 的值不在可移动范围内，会自动移动到可移动范围。<br />默认值：0 |
| damping           | Number   | 阻尼系数，用于控制 x 或 y 改变时的动画和过界回弹的动画，值越大移动越快。<br />默认值：20<br />版本要求：基础库 1.20.0 及以上 |
| friction          | Number   | 摩擦系数，用于控制惯性滑动的动画，值越大摩擦力越大，滑动越快停止；必须大于 0，否则会被设置成默认值。<br />默认值：2<br />版本要求：基础库 1.20.0 及以上 |
| disabled          | Boolean  | 是否禁用。<br />默认值：false                                                               |
| scale             | Boolean  | 是否支持双指缩放，默认缩放手势生效区域是在 `movable-view` 内。<br />默认值：false<br />版本要求：基础库 1.20.0 及以上 |
| scale-min         | Number   | 定义缩放倍数最小值。<br />默认值：0.5<br />版本要求：基础库 1.20.0 及以上                       |
| scale-max         | Number   | 定义缩放倍数最大值。<br />默认值：10<br />版本要求：基础库 1.20.0 及以上                        |
| scale-value       | Number   | 定义缩放倍数，取值范围为 0.5 - 10。<br />默认值：1<br />版本要求：基础库 1.20.0 及以上            |
| animation         | Boolean  | 是否使用动画。<br />默认值：false<br />版本要求：基础库 1.20.0 及以上                          |
| onTouchStart      | EventHandle | 触摸动作开始，事件会向父节点传递。<br />版本要求：基础库 1.11.5 及以上                        |
| catchTouchStart   | EventHandle | 触摸动作开始，事件仅作用于组件，不向父节点传递。<br />版本要求：基础库 1.11.5 及以上          |
| onTouchMove       | EventHandle | 触摸移动事件，事件会向父节点传递。<br />版本要求：基础库 1.11.5 及以上                        |
| catchTouchMove    | EventHandle | 触摸移动事件，事件仅作用于组件，不向父节点传递。<br />版本要求：基础库 1.11.5 及以上          |
| onTouchEnd        | EventHandle | 触摸动作结束，事件会向父节点传递。<br />版本要求：基础库 1.11.5 及以上                        |
| catchTouchEnd     | EventHandle | 触摸动作结束，事件仅作用于组件，不向父节点传递。<br />版本要求：基础库 1.11.5 及以上          |
| onTouchCancel     | EventHandle | 触摸动作被打断，如来电提醒、弹窗。<br />版本要求：基础库 1.11.5 及以上                        |
| onChange          | EventHandle | 拖动过程中触发的事件，`event.detail = {x: x, y: y, source: source}`，其中 `source` 表示产生移动的原因，值可为 `touch`（拖动）。 |
| onChangeEnd       | EventHandle | 拖动结束触发的事件，`event.detail = {x: x, y: y}`。                                       |
| onScale           | EventHandle | 缩放过程中触发的事件，`event.detail = {x, y, scale}`。<br />版本要求：基础库 1.20.0 及以上 |

### `onChange` 返回值 `detail.source`

`source` 字段表示产生移动的原因

| 属性               | 描述                     |
| ------------------ | ------------------------ |
| touch              | 拖动。                   |
| touch-out-of-bounds | 超出移动范围。           |
| out-of-bounds      | 超出移动范围后的回弹。   |
| friction           | 惯性。                   |
| 空字符串           | `setData`。              |

说明：冒泡事件，请查看 [事件介绍](https://opendocs.alipay.com/mini/framework/events) 中的事件类型。
