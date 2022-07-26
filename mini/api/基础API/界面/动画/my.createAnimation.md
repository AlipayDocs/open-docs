# 简介

**my.createAnimation** 是用于创建动画实例 [animation](https://opendocs.alipay.com/mini/api/ui-animation#animation) 的 API。调用实例的方法来描述动画，最后通过动画实例的 `export` 方法将动画数据导出并传递给组件的 `animation` 属性。

## 使用限制

- 调用 `export` 方法后，之前的动画操作将会被清除。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ce24d410ff41e4744d7a39da53b861e6.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/animation?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 


### .js 示例代码
创建一个设置了动画持续时间、动画效果、动画延迟时间、transform-origin 的动画实例示例：
```javascript
//.js
const animation = my.createAnimation({
  transformOrigin: "top right",
  duration: 3000,
  timeFunction: "ease-in-out",
  delay: 100,
})
```
animation 方法示例：
```javascript
// API-DEMO page/API/animation/animation.js
Page({
  onReady() {
    this.animation = my.createAnimation()
  },
  rotate() {
    this.animation.rotate(Math.random() * 720 - 360).step()
    this.setData({ animation: this.animation.export() })
  },
  scale() {
    this.animation.scale(Math.random() * 2).step()
    this.setData({ animation: this.animation.export() })
  },
  translate() {
    this.animation.translate(Math.random() * 100 - 50, Math.random() * 100 - 50).step()
    this.setData({ animation: this.animation.export() })
  },
  skew() {
    this.animation.skew(Math.random() * 90, Math.random() * 90).step()
    this.setData({ animation: this.animation.export() })
  },
  rotateAndScale() {
    this.animation.rotate(Math.random() * 720 - 360)
      .scale(Math.random() * 2)
      .step()
    this.setData({ animation: this.animation.export() })
  },
  rotateThenScale() {
    this.animation.rotate(Math.random() * 720 - 360).step()
      .scale(Math.random() * 2).step()
    this.setData({ animation: this.animation.export() })
  },
  all() {
    this.animation.rotate(Math.random() * 720 - 360)
      .scale(Math.random() * 2)
      .translate(Math.random() * 100 - 50, Math.random() * 100 - 50)
      .skew(Math.random() * 90, Math.random() * 90)
      .step()
    this.setData({ animation: this.animation.export() })
  },
  allInQueue() {
    this.animation.rotate(Math.random() * 720 - 360).step()
      .scale(Math.random() * 2).step()
      .translate(Math.random() * 100 - 50, Math.random() * 100 - 50).step()
      .skew(Math.random() * 90, Math.random() * 90).step()
    this.setData({ animation: this.animation.export() })
  },
  reset() {
    this.animation.rotate3d(0, 0, 0, 0)
      .rotateX(0)
      .rotateY(0)
      .rotateZ(0)
      .scale(1)
      .translate(0, 0)
      .skew(0, 0)
      .step({ duration: 0 })
    this.setData({ animation: this.animation.export() })
  }
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| duration | Integer | 否 | 动画的持续时间，单位 ms，默认值 400。 |
| timeFunction | String | 否 | 定义动画的效果，默认值为 linear。<br />有效值：linear、ease、ease-in、ease-in-out、ease-out、step-start、step-end。 |
| delay | Integer | 否 | 动画延迟时间，单位 ms，默认值 0。 |
| transformOrigin | String | 否 | 设置 transform-origin，默认值为 `50% 50% 0`。 |

## animation
动画实例可以调用以下方法来描述动画，调用结束后会返回实例本身，支持链式调用的写法。view 的 animation 属性初始化为 `{}` 时，在基础库 1.11.0（不包含 1.11.0）及以下版本会报错，建议初始化为 `null`。

### 样式

| **方法** | **参数** | **说明** |
| --- | --- | --- |
| opacity | value | 透明度，参数范围 0~1。 |
| backgroundColor | color | 颜色值。 |
| width | length | 设置宽度：长度值，单位为 px，例如：300 px。 |
| height | length | 设置高度：长度值，单位为 px，例如：300 px。 |
| top | length | 设置 top 值：长度值，单位为 px，例如：300 px。 |
| left | length | 设置 left 值：长度值，单位为 px，例如：300 px。 |
| bottom | length | 设置 bottom 值：长度值，单位为 px，例如：300 px。 |
| right | length | 设置 right 值：长度值，单位为 px，例如：300 px。 |

### 旋转
| **方法** | **参数** | **说明** |
| --- | --- | --- |
| rotate | deg | deg 范围 -180 ~ 180，从原点顺时针旋转一个 deg 角度。 |
| rotateX | deg | deg 范围 -180 ~ 180，在 X 轴旋转一个 deg 角度。 |
| rotateY | deg | deg 范围 -180 ~ 180，在 Y 轴旋转一个 deg 角度。 |
| rotateZ | deg | deg 范围 -180 ~ 180，在 Z 轴旋转一个 deg 角度。 |
| rotate3d | (x, y , z, deg) | 同 [transform-function rotate3d](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/rotate3d)。 |

### 缩放

| **方法** | **参数** | **说明** |
| --- | --- | --- |
| scale | sx,[sy] | 只有一个参数时，表示在 X 轴、Y 轴同时缩放 sx 倍；<br />两个参数时表示在 X 轴缩放 sx 倍，在 Y 轴缩放 sy 倍。 |
| scaleX | sx | 在 X 轴缩放 sx 倍。 |
| scaleY | sy | 在 Y 轴缩放 sy 倍。 |
| scaleZ | sz | 在 Z 轴缩放 sy 倍。 |
| scale3d | (sx,sy,sz) | 在 X 轴缩放 sx 倍，在 Y 轴缩放 sy 倍，在 Z 轴缩放 sz 倍。 |

### 偏移

| **方法** | **参数** | **说明** |
| --- | --- | --- |
| translate | tx,[ty] | 只有一个参数时，表示在 X 轴偏移 tx；<br />有两个参数时，表示在 X 轴偏移 tx，在 Y 轴偏移 ty，单位均为 px。 |
| translateX | tx | 在 X 轴偏移 tx，单位 px。 |
| translateY | ty | 在 Y 轴偏移 ty，单位 px。 |
| translateZ | tz | 在 Z 轴偏移 tz，单位 px。 |
| translate3d | (tx,ty,tz) | 在 X 轴偏移 tx，在 Y 轴偏移 ty，在 Z 轴偏移 tz，单位 px。 |

### 倾斜

| **方法** | **参数** | **说明** |
| --- | --- | --- |
| skew | ax,[ay] | 参数范围 -180 ~ 180。只有一个参数时，Y 轴坐标不变，X 轴坐标延顺时针倾斜 ax 度；两个参数时，分别在 X 轴倾斜 ax 度，在 Y 轴倾斜 ay 度。 |
| skewX | ax | 参数范围 -180 ~ 180。Y 轴坐标不变，X 轴坐标延顺时针倾斜 ax 度。 |
| skewY | ay | 参数范围 -180~180。X 轴坐标不变，Y 轴坐标延顺时针倾斜 ay 度。 |

### 矩阵变形

| **方法** | **参数** | **说明** |
| --- | --- | --- |
| matrix | (a,b,c,d,tx,ty) | 同 [transform-function](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/matrix)。 |
| matrix3d | (a1, b1, c1, d1, a2, b2, c2, d2, a3, b3, c3, d3, a4, b4, c4, d4) | 同 [transform-function matrix3d](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/matrix3d)。 |

### 动画队列

- 调用动画操作方法后，需调用 `step()` 用于表示一组动画完成，在一组动画中可以调用任意多个动画方法，一组动画中的所有动画会同时开始，当一组动画完成后才会进行下一组动画。
- `step()` 可以传入一个跟 `my.createAnimation()` 一样的配置参数用于指定当前组动画的配置。
