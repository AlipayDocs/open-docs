# 简介

在复杂的交互场景下，如果通过 `setData` 去更新视图，体验上可能会比较卡顿。例如，想要实现元素跟随用户手指拖动而移动的效果，需要经过如下响应流程：

1. 用户手指移动，触发基础组件的 `touchMove` 事件，`web-view` 将该事件通信到 `worker`。
2. `worker` 执行该事件回调，并通过 `setData` 更新数据。
3. `web-view` 收到数据更新信息，然后改变元素样式，实现元素移动。

上述过程中，`web-view` 和 `worker` 之间的通信耗时较大，并不能满足对高性能和极速响应的要求。因此，要支持此类富交互场景，我们需要减少通信次数，允许在 `web-view` 侧直接响应事件。SJS 函数支持响应基础组件的事件，无需数据更新，就可以直接驱动视图元素的样式、类名等变更，也可以查询元素的布局信息等。

# 使用限制

- 不支持响应原生组件（如 `map`）和用户自定义组件的事件。
- 响应事件的能力依赖基础库 [2.6.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本。如果基础库版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- `>>>` 选择器依赖基础库 **2.7.3** 或更高版本。如果版本较低，建议采取 **兼容处理**。
- 属性监听的能力依赖基础库 **2.7.7** 或更高版本。如果版本较低，建议采取 **兼容处理**。

## selector 语法

`selector` 类似于 CSS 的选择器，但只支持以下语法：

- ID 选择器：`#the-id`。
- class 选择器（可以连续指定多个）：`.a-class.another-class`。
- 子元素选择器：`.the-parent > .the-child`。
- 后代选择器：`.the-ancestor .the-descendant`。
- 跨自定义组件的后代选择器：`.the-ancestor >>> .the-descendant`（基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持）。
- 多选择器的并集：`#a-node, .some-other-nodes`。

判断 `>>>` 选择器是否可用，可以通过以下代码查询：

```javascript
my.canIUse('sjs.event.selector.deep');
```
# 示例代码

在 `.sjs` 文件中定义函数：

```javascript
// index.sjs
function handleEvent(event, ownerComponent) {
  // currentTarget 的 Descriptor 描述对象
  event.instance.setStyle({
    'font-size': '28rpx',
  });
  // 不往上冒泡，相当于同时调用了
  // event.stopPropagation() 和 
  // event.preventDefault()
  return false;
}

function handlePropChange(newValue, oldValue, ownerComponent, instance) {
  // ...
}

export default {
  handleEvent,
  handlePropChange,
};
```

接着，可以在 `.axml` 中使用这些回调：

```html
<import-sjs from="./index.sjs" name="sjs"></import-sjs>
<view
  data-foo="{{foo}}"
  change:data-foo="{{sjs.handlePropChange}}"
  onTouchStart="{{sjs.handleEvent}}"
></view>
```
# 使用方法

## 事件回调

### 入参

接受两个参数：

| 参数           | 描述                                                                                                 |
| -------------- | ---------------------------------------------------------------------------------------------------- |
| event          | [事件对象](https://opendocs.alipay.com/mini/framework/event-object)，额外地还提供了如下属性：<br />1. instance：event.currentTarget 基础组件的 Descriptor 描述对象。<br />2. preventDefault()：允许阻止原生事件的默认行为。<br />stopPropagation()：行为等同于使用 catch* 事件回调。<br />composedPath()：获取事件路径，基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持。         |
| ownerComponent | 基础组件所在自定义组件/页面的 Descriptor 描述对象。                                              |

#### 1. event.preventDefault()

**Native 渲染引擎**：暂不支持。

对于限定的以下事件：

- touchStart
- touchMove
- touchEnd
- touchCancel

可以通过 event.preventDefault() 阻止 web-view 中的事件默认行为。其他事件（如 tap 等）调用此方法无效。

#### 2. event.stopPropagation()

阻止该事件继续向父基础组件触发。等同于使用了 catch* 事件回调。

#### 3. 自定义组件/页面 Descriptor 描述对象

SJS 函数的第二个参数 ownerComponent 指向该事件 event.currentTarget 所在的自定义组件/页面的 Descriptor 对象，具有如下方法：

| 方法                   | 参数        | 描述                                                                                                               | 渲染引擎兼容性 |
| ---------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------ | ---------------- |
| selectComponent | selector | 选择该自定义组件/页面/基础组件的匹配指定选择器的后代基础组件的 Descriptor 描述对象。selector 选择器字符串。插槽能被提供者选中，而不能被使用者选中。 |仅 WebView |
| selectAllComponents | selector | 选择该自定义组件/页面/基础组件的匹配指定选择器的所有后代基础组件的 Descriptor 描述对象。selector 选择器字符串。插槽能被提供者选中，而不能被使用者选中。 |仅 WebView |
| getState               | -           | 获取状态对象。当有局部变量需要存储起来后续使用时，使用此方法。                                                           | -                |
| callMethod             | (method, arg) | 调用 worker 侧所在自定义组件/页面的自定义方法。<br />1. method 方法名称。<br />2. arg 方法传参。                               | -                |
| requestAnimationFrame  | fn          | 同浏览器平台，仅能被同 Descriptor 对象的 cancelAnimationFrame 取消。返回该请求对应的标识符（可用于取消）。fn 为回调函数。             | 仅 WebView       |
| cancelAnimationFrame   | id          | 取消指定的 `requestAnimationFrame`。仅能取消由该 Descriptor 自己发起的。id 为 `requestAnimationFrame` 返回的标识符。                | 仅 WebView       |
| selectOwnerComponent   | -           | 获取父自定义组件的 Descriptor 描述对象。使用插件时，会跳过选择属于插件的父自定义组件，也会跳过选择属于宿主小程序的父自定义组件。<br />支持基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起。 | 仅 WebView       |
| setTimeout             | (fn, timeout) | 同浏览器平台，仅能由同 Descriptor 对象的 clearTimeout 取消，返回该请求对应的标识符（可用于取消）。<br />1. fn 为回调函数。<br />2. timeout 为超时时间。 | -                |
| clearTimeout           | id          | 取消指定的 `setTimeout`。仅能取消由该 Descriptor 自己发起的。id 为 `setTimeout` 返回的标识符。                                  | -                |
#### 4. 基础组件 Descriptor 描述对象

通过 `event.instance` 可以获得 `event.currentTarget` 的 Descriptor 描述对象，除了上述自定义组件/页面的方法外，还具有如下方法：

| 方法 | 参数 | 描述 | 渲染引擎兼容性 |
| --- | --- | --- | ----- |
| `getComputedStyle` | `props` | 获得相应计算样式值的键值对象。`props` 指定样式属性名的字符串数组。 | 仅 WebView |
| `getBoundingClientRect` | - | 同浏览器平台。 | 仅 WebView |
| `getDataset` | - | 获取基础组件的 `dataset`。与 `event.currentTarget.dataset` 一致。 | - |
| `hasClass` | `className` | 判定是否具有指定样式名。不允许探测以 `a-*` 开头的样式名。`className` 为样式名字符串。 | - |
| `addClass` | `(...classNames)` | 添加指定样式名（可多个），不允许添加以 `a-*` 开头的样式名。 | - |
| `removeClass` | `(...classNames)` | 移除指定样式名（可多个），不允许移除以 `a-*` 开头的样式名。 | - |
| `setStyle` | `style` | 添加指定的行内样式。支持 `rpx`。设置的样式优先级比组件 `axml` 里面定义的样式高。每次调用都会覆盖上一次的调用。<br />`style` 为样式字符串或键值对象。 | - |
| `getDOMProperty` | `properties` | `properties` 为基础元素的 DOM 属性名数组。<br />基础库 2.7.4 起支持。获取基础元素的 DOM 属性。支持的属性如下：<br /><ul><li>`scrollLeft`</li><li>`scrollTop`</li></ul> | 仅 WebView |
| `setDOMProperty` | `properties` | `properties` 为基础元素的 DOM 属性对象。<br />基础库 2.7.4 起支持。设置基础元素的 DOM 属性。支持的属性如下：<br /><ul><li>`scrollLeft`</li><li>`scrollTop`</li></ul> | 仅 WebView |

#### 5. `composedPath()`

基础库 [2.7.3](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持，获取事件路径。返回值为数组，数组的元素为基础元素的 Descriptor 描述对象。使用插件时，宿主小程序内的事件路径会跳过属于插件的描述对象，插件内的事件路径也会跳过属于宿主小程序的描述对象。

### 返回值

当 SJS 函数返回布尔值 `false` 时，等同于同时调用：

- `event.preventDefault()`
- `event.stopPropagation()`

## 属性监听

基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

### 入参

接受四个参数：

| 参数 | 描述 |
| --- | --- |
| `newValue` | 被监听属性的新值。 |
| `oldValue` | 被监听属性的旧值。 |
| `ownerComponent` | 基础组件所在自定义组件/页面的 Descriptor 描述对象。 |
| `instance` | 基础组件的 Descriptor 描述对象。 |

基础组件初始化时会立即回调一次监听函数。当被监听属性值更新后，即新旧值不相等时，会再次触发回调。
