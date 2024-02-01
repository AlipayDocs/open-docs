# 简介

输入框，可设置输入内容的类型、长度、显示形式等。当用户需要输入文字内容时点击文本框，它将自动打开键盘。使用文本字段来请求少量信息。

## 使用限制

- **Native 渲染引擎**：基础库 2.9.7 及以上开始支持。可通过 `my.canIUse('input')` 判断是否支持。
- iOS 系统支付宝客户端版本 10.1.80 以上不支持 `focus="{{true}}"` 自动唤起。
- 小程序中 input 如果父类元素使用了 `position: fixed`，建议加上 `enableNative="{{false}}"`，以解决输入框错位或光标上移问题。在某些情况下，定位问题可能导致光标错位，此时需将 false 改为 true，代码如下：`enableNative="{{true}}"`。
- `confirm-type` 与 `enableNative` 属性存在冲突。若希望 `confirm-type` 生效，则 `enableNative` 不能设置为 false，并且不可设置为 always-system。
- 输入框为同层组件，使用时应注意以下限制：
   - 不支持通过 CSS 修改光标的颜色。

## 扫码体验

![输入框扫码体验](https://gw.alipayobjects.com/zos/skylark/16663486-d067-4b4c-9aed-d746fa3fde46/2018/jpeg/a1d198e6-12e1-43e5-a8a1-cead5a15107a.jpeg)
# 使用

## 在线示例

小程序在线示例可以参考以下链接：[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/input/index&defaultOpenedFiles=pages/input/index&theme=light)。

## 属性

表格中“-”代表支持。

| 属性 | 类型 | 描述 | WebView 兼容性 | Native 兼容性 |
| --- | --- | --- | --- | --- |
| value | String | 初始内容 | - | - |
| name | String | 组件名字，用于表单提交获取数据 | - | - |
| type | String | input 的类型，有效值：`text`、 `number`、 `idcard`、 `digit`（可以唤起带有小数点的数字键盘）、`numberpad`、`digitpad`、`idcardpad`。<br />默认值：`text`<br />**注意：** 当启用数字键盘时，在 Android 客户端上，脱离文档流（如设置了 `float` 或 `position: fixed` 等样式）并指定了 `bottom` 属性的元素会被影响（该元素会被键盘顶起）。可以采用如下方法来暂且避免这个问题：当 input 框聚焦后隐藏被影响的元素 |  基础库 1.13.0+，客户端 10.1.50+<br />支持以下类型：<br />`numberpad`、`digitpad`、`idcardpad`，可通过 [my.canIUse](https://opendocs.alipay.com/mini/api/can-i-use)("input.type.numberpad") 来检测 | 客户端 10.5.56+，支持以下类型：<br />`number`、<br />`idcard`、<br />`digit`、<br />`numberpad`、<br />`digitpad`、<br />`idcardpad` |
| password | Boolean | 是否是密码类型<br />默认值：`false` | - | - |
| placeholder | String | 占位符 | - | - |
| placeholder-style | String | 指定 placeholder 的样式，可设置间距 | 基础库 1.6.0+ | - |
| placeholder-class | String | 指定 placeholder 的样式类 | 基础库 1.6.0+ | - |
| disabled | Boolean | 是否禁用<br />默认值：`false` | - | - |
| maxlength | Number | 最大长度<br />默认值：`140` | - | - |
| focus | Boolean | 获取焦点<br />默认值：`false` | - | - |
| confirm-type | String | 设置键盘右下角按钮的文字，有效值：`done`（显示“完成”）、`go`（显示“前往”）、`next`（显示“下一个”）、`search`（显示“搜索”）、`send`（显示“发送”），平台不同显示的文字略有差异<br />**注意：** 只有在 type=`text` 时有效<br />默认值：`done` | 基础库 1.7.0+ | - |
| confirm-hold | Boolean | 点击键盘右下角按钮时是否保持键盘不收起状态<br />默认值：`false` | 基础库 1.7.0+ | - |
| cursor | Number | 指定 focus 时的光标位置 | - | - |
| selection-start | Number | 获取光标时，选中文本对应的焦点光标起始位置，需要和 selection-end 配合使用<br />默认值：`-1` | 基础库 1.7.0+ | - |
| selection-end | Number | 获取光标时，选中文本对应的焦点光标结束位置，需要和 selection-start 配合使用<br />默认值：`-1` | 基础库 1.7.0+ | - |
| random-number | Boolean | 当 type 为 number, digit, idcard 数字键盘是否随机排列<br />默认值：`false` | 基础库 1.9.0+ | 客户端 10.5.56+ |
| controlled | Boolean | 是否为受控组件。为 true 时，value 内容会完全受 setData 控制<br />建议当 type 值为 text 时不要将 controlled 设置为 true，详见 **Bug & Tip**<br />默认值：`false` | 基础库 1.9.0+ | - |
| always-system | Boolean | 是否强制使用系统键盘和 Web-view 创建的 input 元素。为 true 时，confirm-type、confirm-hold 可能失效<br />默认值：`false` | 基础库 2.7.3+ | 暂不支持 |
| onInput | EventHandle | 键盘输入时触发 input 事件，`event.detail = {value: value, cursor: cursor}`<br />**版本要求**：`cursor` 字段基础库 1.14.0+ | - |
| onConfirm | EventHandle | 点击键盘完成时触发，`event.detail = {value: value}` | - | - |
| onFocus | EventHandle | 聚焦时触发，`event.detail = {value: value}` | - | - |
| onBlur | EventHandle | 失去焦点时触发（仅支持真机），`event.detail = {value: value}` | - | - |

## Bug & Tip

由于部分机型或部分输入法提供联想功能，造成在输入非数字类型的字符时一次输入会连续触发多次 input 事件，且 input 事件的 `event.detail.value` 与用户预期的输入不符，最终导致与 controlled 提供的“受控模式”产生冲突。因此，建议当 type 的值为 `text` 时不要将 controlled 设置为 `true`。
# FAQ

## 如何解决 input 输入框在 iOS 客户端的光标漂移问题？

步骤一：若已在 input 中设置了 `enableNative` 属性，请删除 `enableNative` 属性的全部设置。
步骤二：在 app.json 文件的 window 对象内，设置 `"enableInPageRenderInput": "YES"`。

## 为何 input 输入框聚焦时出现白屏，只有键盘弹出来？

因为使用定位导致键盘将页面 input 内容顶上去了，建议使用 [SearchBar](https://ant-design-mini.antgroup.com/components/input#searchbar-%E6%90%9C%E7%B4%A2%E6%A1%86) 搜索框。
需要判断客户端机型为安卓还是 iOS，然后设置 `enableNative` 属性，并且在 app.json 文件的 window 对象内，设置 `"enableInPageRenderInput": "YES"`。

## 为何 input 输入的内容没有在输入框显示？

如果是因为使用 fixed 定位导致，建议通过设置 `enableNative` 属性解决。

## 小程序 input 输入框获取焦点时会向上推输入框，能否固定？

暂不支持。

## input 输入框弹起键盘有遮挡，影响其他标签控件触发点击事件？

建议修改自定义 [view](/mini/component/view) 样式。

## input 输入框是否支持点击事件，比如 click、tap、touchstart？

目前不支持，可考虑外嵌一层 [view](/mini/component/view)，并利用 view 的 `onTap` 事件实现。

## input 如何用 js 代码清空数据？

需要添加属性 `controlled="{{true}}"`，或在 `onInput` 事件中把输入的值通过 `setData` 方法再赋值给 `value`，再用 `setData` 设置 `value`。

```javascript
// axml
<input class="internet_input" value="{{textValue}}" onInput="keyNum" controlled="{{true}}" type="text" />

// js 清空输入框的方法
keyNum() {
  this.setData({
    textValue: ''
  });
}
```
## input 如何进行监听，如果出现不能监听问题如何解决？

可以使用 input 的 `onInput` 事件监听输入值，通过 `e.detail.value` 打印出输入值进行正则表达式匹配校验。详情请参见示例代码。

## 如何判断 input 的 value 值是不是符合正则表达式？

使用 `var reg = new RegExp("\\w+\\s", "g")`；`getRegExp()` 需要在 SJS 中使用。SJS 脚本不能直接在 JS 中引入调用。

## 父组件如何调用子组件的 input 事件?

详见[组件对象](/mini/framework/component_object)。

## input 内容跳动、延迟如何处理？

可以使用防抖动，示例代码如下：

```javascript
var timer = null;
element.input = function () {
  clearTimeout(timer); // 每次进入时都将之前的定时器清除掉。如果还没到一秒，就将之前的定时器清除掉，这样就不会触发之前 setTimeout 绑定的事件。如果超过一秒，之前的事件就会被触发，下次进来时同样清除之前的 timer。
  timer = setTimeout(function () {
    // 在这里进行操作。这样就不会频繁地进行这里面的操作了。
  }, 1000);
};
```

## 如何在 input 设置了 disabled=true 时，修改 input 的样式？

修改字体颜色，会有灰蒙颜色的效果，可进行以下设置进行修改：

- `placeholder-class` 属性可以通过 ACSS 设置默认占位符的字体颜色。
- 类选择器在 ACSS 中可以设置 input 框的颜色。类选择器可以设置输入的字体颜色。
