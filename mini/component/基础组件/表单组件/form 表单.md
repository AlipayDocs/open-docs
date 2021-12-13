
# 简介
表单。用于将组件内的用户输入的 [textarea](/mini/component/textarea)、 [switch](/mini/component/switch)、 [input](/mini/component/input) 、[checkbox](/mini/component/checkbox)、[slider](/mini/component/slider)、[radio](/mini/component/radio)、[picker](/mini/component/picker) 等组件提交。

## 使用限制

- 预览效果建议以真机为准。
- 目前还不支持 form 表单渲染。
- formId 需要真机调试才会有返回值。
- 当点击 form 表单中 form-type 为 submit 的 [button](/mini/component/button) 组件时，会将表单组件值进行提交，需要在表单组件中加上 name 来作为 key。

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ba69acdbd15ac8dfc96755054c229a2d.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线]( https://herbox-embed.alipay.com/s/doc-form?theme=light&previewZoom=75&chInfo=openhome-doc )

## 示例代码

### .axml 示例代码
```html
<!-- API-DEMO page/component/form/form.axml -->
<view class="page">
  <view class="page-description">表单</view>
  <form onSubmit="onSubmit" onReset="onReset">
    <view class="page-section">
      <view class="page-section-title">Slider</view>
      <view class="page-section-demo">
        <slider value="80" name="slider" show-value />
      </view>
    </view>
    <view class="page-section">
      <view class="form-row">
        <view class="form-row-label">Switch</view>
        <view class="form-row-content" style="text-align: right">
          <switch name="switch" />
        </view>
      </view>
      <view class="form-line" />
      <view class="form-row">
        <view class="form-row-label">Input</view>
        <view class="form-row-content">
          <input name="input" class="input" placeholder="input something" />
        </view>
      </view>
    </view>
    <view class="page-section">
      <view class="page-section-title">Radio</view>
      <view class="page-section-demo">
        <radio-group name="radio-group">
          <label><radio value="radio1" />radio1</label>
          <label><radio value="radio2" />radio2</label>
        </radio-group>
      </view>
    </view>
    <view class="page-section">
      <view class="page-section-title">Checkbox</view>
      <view class="page-section-demo">
        <checkbox-group name="checkbox">
          <label><checkbox value="checkbox1" />checkbox1</label>
          <label><checkbox value="checkbox2" />checkbox2</label>
        </checkbox-group>
      </view>
      <view class="page-section-btns">
        <view><button type="ghost" size="mini" formType="reset">Reset</button></view>
        <view><button type="primary" size="mini" data-id="121" formType="submit">Submit</button></view>
      </view>
    </view>
  </form>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/form/form.js
Page({
  data: {},
  onSubmit(e) {
    my.alert({
      content: `数据：${JSON.stringify(e.detail.value)}`,
    });
  },
  onReset() {
  },
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/form/form.acss */
button + button {
  margin-top: 32rpx;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| report-submit | Boolean | onSubmit 回调是否返回 formId。用于发送 [模板消息](/mini/introduce/message)，使用前可使用 [canIUse](/mini/api/can-i-use) ('form.report-submit')判断是否支持。<br />**注意：** formId 需要真机调试才会有返回值。<br />**版本要求：** 基础库 [1.3.0](/mini/framework/compatibility) 及以上 |
| onSubmit | EventHandle | 携带 form 中的数据触发 submit 事件，`event.detail = {value : {'slider': '80'}, buttonTarget: {'dataset': 'buttonDataset'} }` (可以在 submit 按钮上添加自定义参数)。<br />**版本要求：** buttonTarget 支持基础库 [1.7.0](/mini/framework/compatibility)  及以上 |
| onReset | EventHandle | 表单重置时会触发 reset 事件。 |


# FAQ

### formId 返回值是否可以自定义？
formId 返回值不支持自定义，设置完成对应属性 report-submit 后支付宝返回。

### 支付宝小程序消息推送获取的 formId 有效期是多久？用一次会失效一次吗？
formId 有效期是 7 天，可在 7 天内向用户推送消息。一个 formId 可发送三次

### 小程序接入，付款后调用消息下发返回 formId 为何显示不合法？
商户的模板是表单类型，表单类的模板消息只允许使用表单组件生成的 formId 发送。

### 小程序 form 表单静默触发吗？
不支持，需要用户点击触发。

# 相关文档

- [button 按钮](/mini/component/button)<br />
- [模板消息](https://opendocs.alipay.com/mini/introduce/message)<br />
- [模板消息快速示例](https://opendocs.alipay.com/mini/quick-example/template-message)<br />
