# 简介

输入框，可设置输入内容的类型、长度、显示形式等。当用户需要输入文字内容时点击文本框，它将自动打开键盘。使用文本字段来请求少量信息。

## 使用限制

- iOS 系统支付宝客户端版本 10.1.80 及以上不支持 `focus="{{true}}"` 自动唤起。
- 小程序中 input 如果父类是 `position: fixed`，可以加上 `enableNative="{{false}}"`，解决输入框错位/光标上移问题。个别情况下定位问题会导致光标错位，所以需要把 false 改为 true，代码块为 `enableNative="{{true}}"`。
- confirm-type 与 enableNative 属性冲突，若希望 confirm-type 生效，enableNative 不能设定为 false，而且不能设定 always-system。
- 输入框是同层组件，使用时需要注意以下限制：
   - 不支持通过修改 CSS 来修改光标颜色

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark/16663486-d067-4b4c-9aed-d746fa3fde46/2018/jpeg/a1d198e6-12e1-43e5-a8a1-cead5a15107a.jpeg)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/input/index&defaultOpenedFiles=pages/input/index&theme=light)

## 属性

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| value | String | 初始内容。 |
| name | String | 组件名字，用于表单提交获取数据。 |
| type | String | input 的类型，有效值：`text`、 `number`、 `idcard`、 `digit`(可以唤起带有小数点的数字键盘)、`numberpad`、`digitpad`、 `idcardpad`。<br />**默认值：** text<br />**版本要求：**`numberpad`、`digitpad`、 `idcardpad` 支持基础库 [1.13.0](/mini/framework/compatibility) 客户端 10.1.50 及以上，可通过 <br />[my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use)("input.type.numberpad") 来检测。<br />**注意：** 当启用数字键盘时，在 Android 客户端上，脱离文档流（如设置了 `float` 或 `position: fixed` 等样式）并指定了 `bottom` 属性的元素会被影响（该元素会被键盘顶起）。可以采用如下方法来暂且避免这个问题：当 input 框聚焦后隐藏被影响的元素。 |
| password | Boolean | 是否是密码类型。<br />**默认值：** false |
| placeholder | String | 占位符。 |
| placeholder-style | String | 指定 placeholder 的样式，可设置间距。<br />**版本要求：** 基础库 [1.6.0](/mini/framework/compatibility) 及以上 |
| placeholder-class | String | 指定 placeholder 的样式类。<br />**版本要求：** 基础库 [1.6.0](/mini/framework/compatibility) 及以上 |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| maxlength | Number | 最大长度。<br />**默认值：** 140 |
| focus | Boolean | 获取焦点。<br />**默认值：** false |
| confirm-type | String | 设置键盘右下角按钮的文字，有效值：done（显示“完成”）、go（显示“前往”）、next（显示“下一个”）、search（显示“搜索”）、send（显示“发送”），平台不同显示的文字略有差异。<br />**注意：** 只有在 type=text 时有效。<br />**默认值：** done<br />**版本要求：** 基础库 [1.7.0](/mini/framework/compatibility) 及以上 |
| confirm-hold | Boolean | 点击键盘右下角按钮时是否保持键盘不收起状态。<br />**默认值：** false<br />**版本要求：** 基础库 [1.7.0](/mini/framework/compatibility) 及以上 |
| cursor | Number | 指定 focus 时的光标位置。 |
| selection-start | Number | 获取光标时，选中文本对应的焦点光标起始位置，需要和 selection-end 配合使用。<br />**默认值：** -1<br />**版本要求：** 基础库 [1.7.0](/mini/framework/compatibility) 及以上 |
| selection-end | Number | 获取光标时，选中文本对应的焦点光标结束位置，需要和 selection-start 配合使用。<br />**默认值：** -1<br />**版本要求：** 基础库 [1.7.0](/mini/framework/compatibility) 及以上 |
| random-number | Boolean | 当 type 为 number, digit, idcard 数字键盘是否随机排列。<br />**默认值：** false<br />**版本要求：** 基础库 [1.9.0](/mini/framework/compatibility) 及以上 |
| controlled | Boolean | 是否为受控组件。为 true 时，value 内容会完全受 setData 控制。<br />建议当 type 值为 text 时不要将 controlled 设置为 true，详见 **Bugs & Tips**。<br /><br />**默认值：** false<br />**版本要求：** 基础库 [1.9.0](/mini/framework/compatibility) 及以上 |
| always-system | Boolean | 是否强制使用系统键盘和 Web-view 创建的 input 元素。为 true 时，confirm-type、confirm-hold 可能失效。<br />**默认值**：false<br />**版本要求**：基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上 |
| onInput | EventHandle | 键盘输入时触发 input 事件，`event.detail = {value: value,cursor: cursor}`。<br />**版本要求**：`cursor` 字段基础库 [1.14.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上开始支持。 |
| onConfirm | EventHandle | 点击键盘完成时触发，`event.detail = {value: value}` |
| onFocus | EventHandle | 聚焦时触发，`event.detail = {value: value}`。 |
| onBlur | EventHandle | 失去焦点时触发（仅支持真机），`event.detail = {value: value}`。 |

## Bug & Tip

由于部分机型/部分输入法提供联想功能，造成在输入非数字类型的字符时，一次输入会连续触发多次 input 事件，且 input 事件的 `event.detail.value` 与用户的输入预期不符，最终导致与 controlled 提供的 **受控模式** 产生冲突。因此，建议当 type 值为 text 时不要将 controlled 设置为 true。

# FAQ

## 如何解决 input 输入框在 iOS 客户端的光标漂移问题？

步骤一：若已在 input 中设置了 `enableNative` 属性，删除 `enableNative` 属性的全部设置。<br />步骤二：在 app.json 文件 window 对象内，设置 `"enableInPageRenderInput":"YES"`。

## 为何 input 输入框聚焦的时候出现白屏，只有键盘弹出来？

因为使用定位导致键盘把页面 input 内容顶上去了，建议使用 [SearchBar](https://ant-design-mini.antgroup.com/components/input#searchbar-%E6%90%9C%E7%B4%A2%E6%A1%86) 搜索框。<br />需要判断客户端机型为 安卓还是 iOS，从而设置 `enableNative`属性，然后在 app.json 文件 window 对象内，设置 `"enableInPageRenderInput":"YES"`。

## 为何 input 输入的内容没有在输入框显示？

如果是因为使用 fixed 定位导致， 建议通过设置 `enableNative` 属性解决。

## 小程序 input 输入框获取焦点时会向上推输入框，能否固定？

暂不支持。

## input 输入框弹起键盘有遮挡，影响其他标签控件触发点击事件？

建议修改自定义 [view](/mini/component/view) 样式。

## input 输入框是否支持点击事件，比如 click、tap、touchstart？

暂时不支持，可以考虑外嵌一层 [view](/mini/component/view)，利用 view 的 `onTap` 事件实现。

## input 如何用 js 代码清空数据？

需要添加属性 `controlled="{{true}}"` ，也可以在 `onInput` 事件里把输入的值通过 setData 再赋值给 value，再去 setData 设置 value。

```javascript
//axml
<input class="internet_input" value="{{textValue}}" onInput="keyNum" controlled="{{true}}" type="text"  />
//input如何用js清空
keyNum() {
      this.setData({
        textValue:''
    })
 }
```

## input 如何进行监听，如果出现不能监听问题如何解决？

可以使用 input 的 `onInput` 事件监听输入值，通过 `e.detail.value` 打印出输入值进行正则表达式匹配校验。详情请见示例代码。

## 如何判断 input 的 value 值是不是符合正则表示式？

使用 `var reg = new RegExp("\w+\s", "g")`； getRegExp() 需要在 sjs 中使用。 sjs 脚本不能直接在 js 中引入调用

## 父组件如何调用子组件的 input 事件?

请参见 [组件对象](/mini/framework/component_object)。

## input 内容跳动、延迟如何处理？

可以使用防抖动，示例代码如下：

```javascript
var timer = null;
element.input = function () {
  clearTimeout(timer); // 每次进来的时候都将之前的清除掉，如果还没到一秒的时候就将之前的清除掉，这样就不会触发之前setTimeout绑定的事件， 如果超过一秒，之前的事件就会被触发下次进来的时候同样清除之前的timer
  timer = setTimeout(function () {
    // 在这里进行我们的操作  这样就不会频繁的进行我们这里面的操作了
  }, 1000);
};
```

## 如何在 input 设置了 disabled=true 时，修改 input 的样式 ？

修改字体颜色，会有灰蒙颜色的效果，可进行以下设置进行修改：

- placeholder-class 属性可以通过 acss 设置默认 placeholder 字体颜色。<br />
- class 类选择器在 acss 中可以设置 input 框的颜色，类选择器可以设置输入的字体颜色。<br />
