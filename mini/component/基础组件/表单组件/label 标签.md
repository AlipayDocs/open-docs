
# 简介
用于改进表单组件的可用性。使用 for 属性找到对应组件的 id，或者将组件放在该标签下。当点击时，就会聚焦对应的组件。for 优先级高于内部组件，内部有多个组件的时候默认触发第一个组件。

## 使用限制
label标签不支持onTap、catchTap等点击事件。
目前可以绑定的组件有：[checkbox](component/checkbox)、[radio](component/radio)、[input](component/input)、[textarea](component/textarea)。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark/80846e43-3df4-4711-aa73-04f4af3e70a5/2018/jpeg/a9c328e5-d510-4a26-8595-0cd380313c7c.jpeg#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=128)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-label?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
<!-- API-DEMO page/component/label/label.axml -->
<view class="page">
  <view class="page-section">
    <view class="page-section-title">Checkbox</view>
    <view class="page-section-demo">
      <checkbox-group>
        <view>
          <label>
            <checkbox value="AngularJS" />
            <text> AngularJS</text>
          </label>
        </view>
        <view>
          <label>
            <checkbox value="React" />
            <text> React</text>
          </label>
        </view>
      </checkbox-group>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">Radio</view>
    <view class="page-section-demo">
      <radio-group>
        <view>
          <radio id="AngularJS" value="AngularJS" />
          <label for="AngularJS">AngularJS</label>
        </view>
        <view>
          <radio id="React" value="React" />
          <label for="React">React</label>
        </view>
      </radio-group>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">label中有多个 Checkbox 时，点击 label 关联的元素选择第一个，例如点击的“Click Me”</view>
    <view class="page-section-demo">
      <label>
        <checkbox>选中我</checkbox>
        <checkbox>选不中</checkbox>
        <checkbox>选不中</checkbox>
        <checkbox>选不中</checkbox>
        <view>
          <text>Click Me</text>
        </view>
      </label>
    </view>
  </view>
</view>
```

### .acss 示例代码
```css
/* API-DEMO page/component/label/label.acss */
checkbox-group > view,
radio-group > view {
  margin-bottom: 12rpx;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| for | String | 绑定组件的 ID。 |

