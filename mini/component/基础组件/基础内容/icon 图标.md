
# 简介
图标。

## 使用限制
- icon组件不支持onTap、catchTap等点击事件。
- 跳转页面后左上角显示返回上一页 icon，不支持隐藏。
- icon 中所应用的样式如果是插件中的样式，建议修改样式定义的 `class` 名等信息，否则 icon 中不写插件代码显示正常，添加插件代码 icon 显示不正常。

##  扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/7380714f62c709478a9a507f9ff8450d.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/863388c7-ad35-40db-be75-c84d8ce70b07) 

### .axml 示例代码
```html
<!-- API-DEMO page/component/icon.axml -->
<view class="page">
  <view class="page-description">图标</view>
  <view class="page-section">
    <view class="page-section-title">Type</view>
    <view class="page-section-demo icon-list">
      <block a:for="{{iconType}}">
        <view class="item">
          <icon type="{{item}}" size="45"/>
          <text>{{item}}</text>
        </view>
      </block>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">Size</view>
    <view class="page-section-demo icon-list">
      <block a:for="{{iconSize}}">
        <view class="item">
          <icon type="success" size="{{item}}"/>
          <text>{{item}}</text>
        </view>
      </block>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">Color</view>
    <view class="page-section-demo icon-list">
      <block a:for="{{iconColor}}">
        <view class="item">
          <icon type="success" size="45" color="{{item}}"/>
          <text style="color:{{item}}">{{item}}</text>
        </view>
      </block>
    </view>
  </view>
</view>
```

### .js 示例代码
```js
// API-DEMO page/component/icon.js
Page({
  data: {
    iconSize: [20, 30, 40, 50, 60],
    iconColor: [
      'red', 'yellow', 'blue', 'green',
    ],
    iconType: [
      'success',
      'info',
      'warn',
      'waiting',
      'clear',
      'success_no_circle',
      'download',
      'cancel',
      'search',
    ],
  },
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/icon.acss */
.icon-list {
  display: -webkit-flex;
  display: flex;
  -webkit-flex-wrap: wrap;
  flex-wrap: wrap;
}
.item {
  display: -webkit-flex;
  display: flex;
  flex-direction: column;
  -webkit-flex-direction: column;
  margin-bottom: 10px;
  margin-right: 10px;
  align-items: center;
  -webkit-align-items: center;
}
```

## 属性
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | icon 类型。有效值： info、warn、waiting、cancel、download、search、clear、success、success_no_circle、loading。<br />**版本要求：** loading 支持基础库 [1.7.2](/mini/framework/compatibility) 及以上 |
| size | Number | icon 大小，单位 px。<br />**默认值：** 23 |
| color | String | icon 颜色，同 CSS 色值。 |

