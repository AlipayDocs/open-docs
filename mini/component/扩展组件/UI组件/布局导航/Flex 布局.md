这篇文档介绍了如何在小程序中使用 CSS Flex 布局的封装。首先提供了二维码扫描体验的图像。随后，链接了一个小程序的在线体验平台 Herbox，并提供了一个 .json 配置文件示例代码，说明如何在小程序的配置文件中使用 Flex 相关的组件。
### .axml 示例代码

```html
<view class="flex-container">
  <view class="sub-title">基础</view>
  <flex>
    <flex-item><view class="placeholder">区块</view></flex-item>
    <flex-item><view class="placeholder">区块</view></flex-item>
  </flex>
  <view style="height: 20px;" />
  <flex>
    <flex-item><view class="placeholder">区块</view></flex-item>
    <flex-item><view class="placeholder">区块</view></flex-item>
    <flex-item><view class="placeholder">区块</view></flex-item>
  </flex>
  <view style="height: 20px;" />
  <flex>
    <flex-item><view class="placeholder">区块</view></flex-item>
    <flex-item><view class="placeholder">区块</view></flex-item>
    <flex-item><view class="placeholder">区块</view></flex-item>
    <flex-item><view class="placeholder">区块</view></flex-item>
  </flex>
  <view class="sub-title">换行</view>
  <flex wrap="wrap">
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
  </flex>
  <view class="sub-title">对齐</view>
  <flex justify="center">
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
  </flex>
  <flex justify="end">
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
  </flex>
  <flex justify="between">
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline">区块</view>
  </flex>
  <flex align="start">
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline small">区块</view>
    <view class="placeholder inline">区块</view>
  </flex>
  <flex align="end">
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline small">区块</view>
    <view class="placeholder inline">区块</view>
  </flex>
  <flex align="baseline">
    <view class="placeholder inline">区块</view>
    <view class="placeholder inline small">区块</view>
    <view class="placeholder inline">区块</view>
  </flex>
</view>
```

- 在 flex 容器（`<flex>`）中，每个 `<flex-item>` 排布 `view` 类的子元素。
- 使用 `style="height: 20px;"` 创建视觉上的纵向空间。
- 通过设置 `wrap`、`justify` 和 `align` 属性，来控制区块的对齐和排布方式。

**注：** 英文词汇 `Basic`、`Wrap` 和 `Align` 均被翻译为中文词汇 `基础`、`换行` 和 `对齐`。代码中的注释被移到了正文中，以保持代码的干净整洁。代码内容本身未做修改以保持功能不变。
```css
.flex-container {
  padding: 10px;
}
.sub-title {
  color: #888;
  font-size: 14px;
  padding: 30px 0 18px 0;
}
.placeholder {
  background-color: #ebebef;
  color: #bbb;
  text-align: center;
  height: 30px;
  line-height: 30px;
  width: 100%;
}
.placeholder.inline {
  width: 80px;
  margin: 9px 9px 9px 0;
}
.placeholder.small {
  height: 20px;
  line-height: 20px;
}
```


```javascript
Page({});
```
## 属性说明

Flex 帜局是通过 `flex` 和 `flex-item` 两种标签组合使用的，对应的属性值有所不同。

| 属性         | 类型   | 必填  | 描述 |
| --------- | ---- | ---- | --- |
| direction | String | 否    | 项目定位方向。可选值：`row`、`row-reverse`、`column`、`column-reverse`。默认值：`row` |
| wrap      | String | 否    | 子元素的换行方式。可选值：`nowrap`、`wrap`、`wrap-reverse`。默认值：`nowrap` |
| justify   | String | 否    | 子元素在主轴上的对齐方式。可选值：`start`、`end`、`center`、`between`、`around`。默认值：`start` |
| align     | String | 否    | 子元素在交叉轴上的对齐方式。可选值：`start`、`center`、`end`、`baseline`、`stretch`。默认值：`center` |
| alignContent | String | 否 | 有多根轴线时的对齐方式。可选值：`start`、`end`、`center`、`between`、`around`、`stretch`。默认值：`stretch` |

## flex-item

`flex-item` 组件默认应用了样式 `flex:1`，确保所有 item 平均分配宽度。`flex` 容器的 children 并不一定是 `flex-item`。
