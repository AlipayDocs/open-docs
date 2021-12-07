
# 简介
单选框。具体用法和小程序框架中 radio 保持一致，在 radio 基础上做了样式的封装。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*2rsaS7d71tMAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=PuXwXDEBDTUYO98u1wbhSAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-am-radio?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "am-radio",
 "usingComponents": {
   "am-radio": "mini-ali-ui/es/am-radio/index",
   "list": "mini-ali-ui/es/list/index",
   "list-item": "mini-ali-ui/es/list/list-item/index"
 }
}
```

### .axml 示例代码
```html
<view class="page">
 <view class="page-description">单选框</view>
 <view class="page-section">
   <view class="section section_gap">
     <form onSubmit="onSubmit" onReset="onReset">
       <view class="page-section-demo">
         <radio-group class="radio-group" onChange="radioChange" name="lib">
           <label class="radio" a:for="{{items}}" key="label-{{index}}">
             <am-radio value="{{item.value}}" checked="{{item.checked}}" disabled="{{item.disabled}}" />
             <view style="display:inline-block;">{{item.desc}}</text>
           </label>
         </radio-group>
       </view>
       <view class="page-section-demo">
         <radio-group class="radio-group" onChange="radioChange" name="lib">
           <label class="radio" a:for="{{items1}}" key="label-{{index}}">
             <am-radio value="{{item.value}}" checked="{{item.checked}}" disabled="{{item.disabled}}" />
             <view style="display:inline-block;">{{item.desc}}</text>
           </label>
         </radio-group>
       </view>
     </form>
   </view>
 </view>
</view>
```

### .js 示例代码
```javascript
Page({
 data: {
   items: [
     { checked: true, disabled: false, value: 'a', desc: '单选框-默认选中', id: 'checkbox1' },
     { checked: false, disabled: false, value: 'b', desc: '单选框-默认未选中', id: 'checkbox2' },
   ],
   items1: [
     { checked: true, disabled: true, value: 'c', desc: '单选框-默认选中disabled', id: 'checkbox3' },
   ],
 },
 radioChange() {
 },
});
```

### .acss 示例代码
```css
.radio {
 display: flex; align-items: center;
}
.page-section-demo {
 padding: 24rpx;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| value | String | 组件值，选中时 change 事件会携带的 value。 |
| checked | Boolean | 当前是否选中，可用来设置默认选中。<br />**可选值：** true、false。<br />**默认值：** false |
| disabled | Boolean | 是否禁用。<br />**可选值：** true、false。<br />**默认值：** false |
| id | String | 与 label 组件的 for 属性组合使用。 |

