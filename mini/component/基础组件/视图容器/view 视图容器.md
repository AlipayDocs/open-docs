
# 简介
**view 视图容器** 组件实现了在小程序界面内插入一个可以容纳其他任何元素的视图块，类似于 HTML 语言的 `<div>` 元素 。

## 使用限制

- view 组件可通过固定宽度或者高度，使用 overflow-x 或者 overflow-y 设置为 scroll 属性进行滚动，也可通过 [scroll-view](/mini/component/scroll-view) 制作滚动视图。
- view 组件不支持覆盖 map 组件，可通过同层渲染实现 [cover-view](https://opendocs.alipay.com/mini/component/cover-view) 覆盖 [map](https://opendocs.alipay.com/mini/component/map) 组件。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark/0d7e6d33-189a-49db-ad0b-ad2cf678cc6b/2018/jpeg/73929592-3352-4b3e-a6be-008512ed01a1.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-view?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .axml 示例代码
```html
<!-- API-DEMO page/component/view.axml -->
<view class="page">
  <view>
    <button a:if="{{returnIndex}}" onTap="returnIndex">回到首页</button>
  </view>
  <view class="page-description">视图容器，相当于 web 的 div 或者 react-native 的 View。</view>
  <view class="page-section">
    <view class="page-section-demo">
      <view class="stream">
        <view class="post">
          <view class="postUser">
            <view class="postUser__name">Chris</view>
          </view>
          <view class="postBody">
            <view class="postBody__content">
              欢迎使用支付宝小程序！！！
            </view>
            <view class="postBody__date">
              May 20
            </view>
          </view>
        </view>
        <view class="post">
          <view class="postUser">
            <view class="postUser__name">Jack</view>
          </view>
          <view class="postBody">
            <view class="postBody__content">
              @Chris 我该如何上手？
            </view>
            <view class="postBody__date">
              May 21
            </view>
          </view>
        </view>
        <view class="post">
          <view class="postUser">
            <view class="postUser__name">Chris</view>
          </view>
          <view class="postBody">
            <view class="postBody__content">
              你可以查看 Demo，对小程序有一个简单的了解；然后下载我们的 IDE 进行开发。
            </view>
            <view class="postBody__date">
              May 22
            </view>
          </view>
        </view>
        <view class="post">
          <view class="postUser">
            <view class="postUser__name">Jessie</view>
          </view>
          <!-- hover red -->
          <view class="postBody" hover-class="red">
            <view class="postBody__content">
              赞!
            </view>
            <view class="postBody__date" hidden>
              June 1
            </view>
          </view>
        </view>
        <view class="post" hidden>
          <view class="postUser">
            <view class="postUser__name">Jessie</view>
          </view>
          <view class="postBody">
            <view class="postBody__content">
              赞! +1
            </view>
            <view class="postBody__date">
              June 1
            </view>
          </view>
        </view>
      </view>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/view.js
Page({
  data: {
    pageName: 'component/view',
  },
  onLoad() {
    this.setData({
      returnIndex: getCurrentPages().length === 1,
    })
  },
  returnIndex() {
    my.switchTab({ url: '/page/component/index' });
  },
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/view.acss */
.post + .post {
  margin-top: 10rpx;
}
.post {
  display: flex;
}
.postUser {
  flex: 0 1 auto;
  padding-bottom: 20rpx;
}
.postUser__name {
  width: 180rpx;
  color: #57727C;
  font-size: 24rpx;
  font-weight: 700;
  line-height: 1;
  text-align: center;
  margin-top: 60rpx;
}
.postBody {
  flex: 1 1 0%;
  position: relative;
  padding: 30rpx;
  border: 2rpx solid #CAD0D2;
  border-radius: 8rpx;
}
.postBody:after,
.postBody:before {
  right: 100%;
  top: 70rpx;
  border: solid transparent;
  content: " ";
  height: 0;
  width: 0;
  position: absolute;
  pointer-events: none;
}
.postBody:after {
  border-color: transparent;
  border-right-color: #ffffff;
  border-width: 16rpx;
  margin-top: -16rpx;
}
.postBody:before {
  border-color: transparent;
  border-right-color: #CAD0D2;
  border-width: 18rpx;
  margin-top: -18rpx;
}
.postBody__content {
  color: #57727C;
  font-size: 24rpx;
}
.postBody__date {
  margin-top: 10rpx;
  color: #86969C;
  font-size: 20rpx;
  text-transform: uppercase;
  letter-spacing: 2rpx;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| disable-scroll | Boolean | 是否阻止区域内滚动页面。<br />**默认值：** false<br />**说明：** 如果 view 中嵌套 view，外层 view 设置 `disable-scroll` 为 true 时禁止内部的滚动。 |
| hover-class | String | 触摸时添加的样式类。 |
| hover-start-time | Number | 按住多久后出现点击状态，单位毫秒。 |
| hover-stay-time | Number | 松开后点击状态保留时间，单位毫秒。 |
| hidden | Boolean | 是否隐藏。<br />**默认值：** false |
| class | String | 自定义样式名。 |
| style | String | 内联样式。 |
| animation | Object | 用于动画，详见 [my.createAnimation](api/ui-animation#mycreateanimation) 。使用 `my.createAnimation` 生成的动画是通过过渡（Transition）实现的，只会触发 `onTransitionEnd`，不会触发 `onAnimationStart`, `onAnimationIteration`, `onAnimationEnd`。<br />**默认值：**{} |
| hover-stop-propagation | Boolean | 是否阻止当前元素的祖先元素出现点击态。<br />**默认值：** false<br />**版本要求：** 基础库 [1.10.0](/mini/framework/compatibility) 及以上 |
| onTap | EventHandle | 点击。 |
| onTouchStart | EventHandle | 触摸动作开始。 |
| onTouchMove | EventHandle | 触摸后移动。 |
| onTouchEnd | EventHandle | 触摸动作结束。 |
| onTouchCancel | EventHandle | 触摸动作被打断，如来电提醒，弹窗。 |
| onLongTap | EventHandle | 长按 500ms 之后触发，触发了长按事件后进行移动将不会触发屏幕的滚动。 |
| onTransitionEnd | EventHandle | 过渡（Transition）结束时触发。<br />**版本要求：** 基础库 [1.8.0](/mini/framework/compatibility) 及以上 |
| onAnimationIteration | EventHandle | 每开启一次新的动画过程时触发。（第一次不触发）<br />**版本要求：** 基础库 [1.8.0](/mini/framework/compatibility) 及以上 |
| onAnimationStart | EventHandle | 动画开始时触发。<br />**版本要求：** 基础库 [1.8.0](/mini/framework/compatibility) 及以上 |
| onAnimationEnd | EventHandle | 动画结束时触发。<br />**版本要求：** 基础库 [1.8.0](/mini/framework/compatibility) 及以上 |
| onAppear | EventHandle | 当前元素可见面积超过50%时触发。<br />**版本要求：** 基础库 [1.9.0](/mini/framework/compatibility) 及以上 |
| onDisappear | EventHandle | 当前元素不可见面积超过50%时触发。<br />**版本要求：** 基础库 [1.9.0](/mini/framework/compatibility) 及以上 |
| onFirstAppear | EventHandle | 当前元素首次可见面积达到50%时触发。<br />**版本要求：** 基础库 [1.9.4](/mini/framework/compatibility) 及以上 |
| role | - | 表示组件的语义角色。设置为 img 时，组件聚焦后读屏软件会朗读出 **图像** ；设置为 button 时，聚焦后读屏软件会朗读出 **按钮** 。详情请参见 [aria-component](https://opendocs.alipay.com/mini/component/accessibility)。 |


# FAQ

## 如何改变 view 的展示顺序？
将这两个模块嵌入到一个循环里面，每一个循环的小模块加一个类型值进行标识。

## 页面滚动时在不同屏幕滚动到的位置不同，如何解决？
可使用 [my.pageScrollTo](https://opendocs.alipay.com/mini/api/scroll) 的 selector 选择，给需要滚动的元素定义一个 id 或者 class，打开页面后会自动滚动到该元素位置。 
