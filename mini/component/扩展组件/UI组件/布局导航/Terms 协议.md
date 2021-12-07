
# 简介
需用户主动操作后，才能开通或激活服务时；通常包含了用户授权协议详细说明的跳转入口。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*goE_Sa_KX1oAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=lsHNmXXKvxl4XsA2_djixAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-terms?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码
```json
{
   "defaultTitle": "Terms",
   "usingComponents": {
     "terms": "mini-ali-ui/es/terms/index"
   }
}
```

### .axml 示例代码
```html
<view>
 <terms onSelect="onSelect" related="{{c1.related}}" hasDesc="{{c1.hasDesc}}" agreeBtn="{{c1.agreeBtn}}" cancelBtn="{{c1.cancelBtn}}">
   <view class="text" slot="header">
     <text>
       同意
       <navigator class="link" url="https://m.alipay.com">《用户授权协议》</navigator>
     </text>
   </view>
 </terms>
 <text class="title">双按钮</text>
</view>
<view>
 <terms onSelect="onSelect" fixed="{{c2.fixed}}" related="{{c2.related}}" hasDesc="{{c2.hasDesc}}" agreeBtn="{{c2.agreeBtn}}" cancelBtn="{{c2.cancelBtn}}" shape="{{c2.shape}}" capsuleMinWidth="{{c2.capsuleMinWidth}}" capsuleSize="{{c2.capsuleSize}}">
   <view class="text" slot="desc">
     <text>
       查看
       <navigator class="link" url="https://m.alipay.com">《ETC服务用户协议》</navigator>
       ，授权ETC服务获取身份证、收货地址用于申请ETC，关注车主服务生活号获取审核；
     </text>
   </view>
 </terms>
 <text class="title">带辅助描述</text>
</view>
<view>
 <terms onSelect="onSelect" fixed="{{c3.fixed}}" related="{{c3.related}}" hasDesc="{{c3.hasDesc}}" agreeBtn="{{c3.agreeBtn}}" cancelBtn="{{c3.cancelBtn}}">
   <view class="text" slot="header">
     <text>
       同意
       <navigator class="link" url="https://m.alipay.com">《用户授权协议》</navigator>
     </text>
   </view>
 </terms>
 <text class="title">捆绑协议已选中</text>
</view>
<view>
 <terms onSelect="onSelect" fixed="{{c4.fixed}}" related="{{c4.related}}" hasDesc="{{c4.hasDesc}}" agreeBtn="{{c4.agreeBtn}}" cancelBtn="{{c4.cancelBtn}}" shape="{{c4.shape}}" capsuleMinWidth="{{c4.capsuleMinWidth}}" capsuleSize="{{c4.capsuleSize}}">
   <view class="text" slot="header">
     <text>
       同意
       <navigator class="link" url="https://m.alipay.com">《用户授权协议》</navigator>
     </text>
   </view>
 </terms>
 <text class="title">捆绑协议未选中</text>
</view>
<view>
 <terms fixed="{{c5.fixed}}" related="{{c5.related}}" hasDesc="{{c5.hasDesc}}"  agreeBtn="{{c5.agreeBtn}}" cancelBtn="{{c5.cancelBtn}}" shape="{{c5.shape}}" capsuleMinWidth="{{c5.capsuleMinWidth}}" capsuleSize="{{c5.capsuleSize}}">
   <view class="text" slot="header">
     <text>
       同意
       <navigator class="link" url="https://m.alipay.com">《用户授权协议》</navigator>
     </text>
   </view>
 </terms>
 <text class="title">无捆绑协议</text>
</view>
<view style="padding-bottom:30px;">
 <terms fixed="{{c6.fixed}}" related="{{c6.related}}" hasDesc="{{c6.hasDesc}}" agreeBtn="{{c6.agreeBtn}}" cancelBtn="{{c6.cancelBtn}}" shape="{{c6.shape}}" capsuleMinWidth="{{c6.capsuleMinWidth}}" capsuleSize="{{c6.capsuleSize}}">
   <view class="text" slot="header">
     <text>
       同意
       <navigator class="link" url="https://m.alipay.com">《用户授权协议》</navigator>
     </text>
   </view>
 </terms>
 <text class="title">吸底</text>
</view>
```

### .acss 示例代码
```css
.title{
   text-align: center;
   display: block;
   width: 100%;
   margin: 20px 0;
}
page {
   padding: 24px  12px;
}
```

### .js 示例代码
```
const cfg = {
 c1: {
   related: false,
   agreeBtn: {
     title: '同意协议并开通',
   },
   cancelBtn: {
     title: '暂不开通，仅手动缴费',
   },
   hasDesc: false,
 },
 c2: {
   related: false,
   agreeBtn: {
     title: '同意协议并开通',
   },
   hasDesc: true,
 },
 c3: {
   related: true,
   agreeBtn: {
     checked: true,
     title: '提交',
   },
 },
 c4: {
   related: true,
   agreeBtn: {
     title: '提交',
   },
 },
 c5: {
   related: false,
   agreeBtn: {
     title: '同意协议并提交',
   },
 },
 c6: {
   related: true,
   fixed: true,
   agreeBtn: {
     checked: true,
     title: '提交',
   },
 },
};
Page({
 data: cfg,
 onLoad() {
 },
 onSelect(e) {
   const selectedData = e.currentTarget.dataset.name || '';
   selectedData && my.alert({
     title: 'Terms Btns',
     content: selectedData,
   });
 },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| fixed | Boolean | 需要常驻页面底部。<br />**可选值：** true、false。<br />**默认值：** false |
| related | Boolean | 是否需要勾选复选框。<br />**可选值：** true、false。<br />**默认值：** true |
| agreeBth | Object | 同意按钮配置。<br />**默认值：** {"title":"", "subtitle":"", "type":"primary", "data":1, "checked":false } |
| cancelBtn | Object | 取消按钮配置。<br />**默认值：** {"title":"", "subtitle":"", "type":"default", "data":2 } |
| capsuleSize | String | 胶囊按钮大小。<br />**可选值：** large、medium、small。<br />**默认值**：medium |
| shape | String | 按钮形状。<br />**可选值：** default, capsule。<br />**默认值**：default |
| capsuleMinWidth | Boolean | 是否启用胶囊按钮最小宽度。<br />**可选值：** true、false。<br />**默认值：** false |
| hasDesc | Boolean | 是否有协议相关的描述信息。<br />**可选值：** true、false。<br />**默认值：** false |
| onSelect | EventHandle | 点击按钮事件。 |

