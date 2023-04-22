## 说明
- formId 只能由真机生成，IDE 生成的不可用。
- from 表单设置 `report-submit="{{true}}"`，通过 button 触发表单提交 onSubmit 事件才会返回 formId。
- 当前小程序应用前端生成的 formId 只能用于当前小程序应用的模板消息发送，即A小程序前端生成的 formId 不能用于 B 小程序后端调用接口发送模板消息。
- 建议 form 表单内至少有一个表单组件（ [textarea](https://opendocs.alipay.com/mini/component/textarea)、 [switch](https://opendocs.alipay.com/mini/component/switch)、 [input](https://opendocs.alipay.com/mini/component/input) 、[checkbox](https://opendocs.alipay.com/mini/component/checkbox)、[slider](https://opendocs.alipay.com/mini/component/slider)、[radio](https://opendocs.alipay.com/mini/component/radio)、[picker](https://opendocs.alipay.com/mini/component/picker) 等）并在表单组件中加上 name 来作为 key 提交。

### 获取示例代码
```html
//.axml
<form onSubmit="onSubmit" report-submit="{{true}}">  
  <input name="input" placeholder="input something" value="test" />
  <button type="primary" size="mini" formType="submit">Submit</button>
</form>
```
```javascript
//.js
Page({ 
  onSubmit(e){ 
    console.log(e.detail.formId)//返回formId值：MjA4ODYwMjAwMDY2MDQ2NF8xNTkzNTcyNTQ2NDI3Xzg2Nw==  }})
```

## 相关文档

- [form组件](https://opendocs.alipay.com/mini/component/form)
- [消息](https://opendocs.alipay.com/mini/introduce/message)

 <br /> 
