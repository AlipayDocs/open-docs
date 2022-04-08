# 简介
当页面在请求数据过程中，会出现信息读取的进度过程。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark/97c38fce-1453-4d80-b1e0-c35812f56167/2018/jpeg/6df7d4cf-70e6-438f-b8c4-ef613de4005e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-progress?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
<!-- API-DEMO page/component/progress.axml -->
<view class="page">
  <view class="page-description">进度条</view>
  <view class="page-section">
    <view class="page-section-demo">
      <progress percent="20" show-info/>
      <progress percent="40" active/>
      <progress percent="60" stroke-width="10"/>
      <progress percent="80" active-Color="#6abf47" backgroundColor="#f4333c" />
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/progress.js
Page({});
```

### .acss 示例代码
```css
/* API-DEMO page/component/progress.acss */
progress{
  margin-bottom: 60rpx;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| percent | Float | 百分比(0~100)。 |
| show-info | Boolean | 在右侧显示百分比值。<br />**默认值：** show-info="{{false}}" |
| stroke-width | Number | 线的粗细，单位 px。<br />**默认值：** 6 |
| active-color | Color | 已选择的进度条颜色。<br />**默认值：** #09BB07 |
| background-color | Color | 未选择的进度条颜色。 |
| active | Boolean | 是否添加从 0% 开始加载的入场动画。<br />**默认值：** `active="{{false}}"` |

