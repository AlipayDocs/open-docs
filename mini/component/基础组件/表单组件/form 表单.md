# 简介

表单。用于将组件内的用户输入，如 [textarea](https://opendocs.alipay.com/mini/component/textarea)、[switch](https://opendocs.alipay.com/mini/component/switch)、[input](https://opendocs.alipay.com/mini/component/input)、[checkbox](https://opendocs.alipay.com/mini/component/checkbox)、[slider](https://opendocs.alipay.com/mini/component/slider)、[radio](https://opendocs.alipay.com/mini/component/radio)、[picker](https://opendocs.alipay.com/mini/component/picker) 等组件提交。

## 使用限制

- 预览效果建议以真机为准。
- 目前，还不支持 form 表单渲染。
- formId 需要真机调试才会有返回值。
- 当点击表单中 form-type 为 submit 的 [button](https://opendocs.alipay.com/mini/component/button) 组件时，会提交表单组件的值。需要在表单组件中加上 name 作为 key。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ba69acdbd15ac8dfc96755054c229a2d.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/form/index&defaultOpenedFiles=pages/form/index&theme=light)

## 属性说明

| 属性          | 类型     | 描述 |
| ------------- | -------- | --- |
| report-submit | Boolean  | onSubmit 回调是否返回 formId，用于发送[消息](https://opendocs.alipay.com/mini/repo-01emf6)。使用前可用 [canIUse](https://opendocs.alipay.com/mini/api/can-i-use)('form.report-submit') 判断是否支持。<br />**注意：**formId 需要真机调试才会有返回值。<br />**版本要求：**基础库 [1.3.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onSubmit       | EventHandle | 携带 form 中的数据触发 submit 事件，`event.detail = { value: { 'slider': '80' }, buttonTarget: { 'dataset': 'buttonDataset' } }`（可在 submit 按钮上添加自定义参数）。<br />**版本要求：**buttonTarget 支持基础库 [1.7.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onReset        | EventHandle | 表单重置时会触发 reset 事件。 |

# 常见问题

### formId 返回值是否支持自定义？

formId 的返回值不支持自定义。设置对应属性 report-submit 后，由支付宝返回。

### 支付宝小程序消息推送获取的 formId 有效期是多久？用一次会失效一次吗？

formId 的有效期是 7 天，可以在 7 天内向用户推送消息。一个 formId 可发送三次。

### 为何小程序接入后，付款调用消息下发返回的 formId 显示不合法？

商户的模板为表单类型，表单类的模板消息只允许使用表单组件生成的 formId 发送。

### 小程序 form 表单是否支持静默触发？

不支持，需要用户点击来触发。
