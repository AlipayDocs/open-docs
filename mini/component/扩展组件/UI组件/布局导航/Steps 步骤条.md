# 简介

根据步骤显示的进度条。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*rxAHT4dTIvcAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=KYBuhWlZKyz_rIAo-puidwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-steps?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Steps",
  "usingComponents": {
    "steps": "mini-ali-ui/es/steps/index"
  }
}
```

### .axml 示例代码

```html
<steps
  className="demo-steps-class"
  activeIndex="{{activeIndex}}"
  failIndex="{{failIndex}}"
  items="{{items}}"
>
  <view slot="title_2" style="color: green; font-weight: bold;"
    >titile 的内容</view
  >
</steps>
<steps
  className="demo-steps-class"
  activeIndex="{{activeIndex}}"
  failIndex="{{failIndex}}"
  horizHighlight="{{true}}"
  items="{{items2}}"
>
  <view slot="title_2" style="color: green; font-weight: bold;"
    >titile 的内容</view
  >
  <view slot="desc_4"
    >当前 item 没有 <text style="color: green;">description</text> 时，使用 slot
    内容。</view
  >
</steps>
<steps
  className="demo-steps-class"
  direction="vertical"
  failIndex="{{failIndex}}"
  activeIndex="{{activeIndex}}"
  items="{{items2}}"
  size="{{size}}"
  showStepNumber="{{showNumberSteps}}"
>
  <view slot="title_2" style="color: green; font-weight: bold;"
    >titile 的内容</view
  >
  <view slot="desc_4"
    >当前 item 没有 <text style="color: green;">description</text> 时，使用 slot
    内容。</view
  >
</steps>
<view class="demo-btn-container">
  <button class="demo-btn" onTap="preStep">上一步</button>
  <button class="demo-btn" onTap="nextStep">下一步</button>
</view>
<view class="demo-btn-container">
  <button class="demo-btn" onTap="setFailIndex">设置错误项</button>
  <button class="demo-btn" onTap="cancelFailIndex">取消错误项</button>
</view>
<view class="demo-btn-container">
  <button class="demo-btn" onTap="setIconSizeAdd">设置图标大小+</button>
  <button class="demo-btn" onTap="setIconSizeReduce">设置图标大小-</button>
</view>
<button type="primary" onTap="showNumberList">
  以{{!showNumberSteps?'数字':'图片/icon'}}方式展示步骤序列
</button>
```

### .js 示例代码

```javascript
Page({
  data: {
    activeIndex: 1,
    failIndex: 0,
    size: 0,
    items: [
      {
        title: '步骤1',
      },
      {
        title: '步骤2',
      },
      {
        title: '步骤3',
      },
    ],
    items2: [
      {
        title: '步骤1',
        description:
          '这是步骤1的描述文档，文字足够多的时候会换行，设置了成功的icon',
        activeIcon: 'https://i.alipayobjects.com/common/favicon/favicon.ico',
        size: 20,
      },
      {
        title: '步骤2 如果标题足够长的话也会换行的',
        description: '这是步骤2，同时设置了两种状态的icon',
        icon: 'https://gw.alipayobjects.com/mdn/miniProgram_mendian/afts/img/A*lVojToO-qZIAAAAAAAAAAABjAQAAAQ/original',
        activeIcon: 'https://i.alipayobjects.com/common/favicon/favicon.ico',
      },
      {
        title: '步骤3',
        description: '这是步骤3',
      },
      {
        title: '步骤4',
      },
    ],
    showNumberSteps: true,
  },
  nextStep() {
    this.setData({
      activeIndex: this.data.activeIndex + 1,
    });
  },
  preStep() {
    this.setData({
      activeIndex: this.data.activeIndex - 1,
    });
  },
  setFailIndex() {
    this.setData({
      failIndex: 3,
    });
  },
  cancelFailIndex() {
    this.setData({
      failIndex: 0,
    });
  },
  setIconSizeAdd() {
    this.setData({
      size:
        this.data.size < 30 && this.data.size > 14 ? this.data.size + 1 : 15,
    });
  },
  setIconSizeReduce() {
    this.setData({
      size: this.data.size > 15 ? this.data.size - 1 : 15,
    });
  },
  showNumberList() {
    this.setData({
      showNumberSteps: !this.data.showNumberSteps,
    });
  },
});
```

### .acss 示例代码

```css
.demo-steps-class {
  margin: 20px 0;
  border-bottom: 1px solid #e5e5e5;
}
.demo-btn-container {
  display: flex;
  justify-content: space-between;
  margin: 20px;
}
.demo-btn {
  width: 47%;
}
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 最外层覆盖样式。 |
| activeIndex | Number | true | 当前激活步骤。<br />**默认值：** 1 |
| failIndex | Number | false | 当前失败步骤（只在 vertical 模式下生效）。<br />**默认值：** 0 |
| direction | String | false | 显示方向，可选值：vertical、horizontal。<br />**默认值：** horizontal |
| size | Number | false | 统一的 icon 大小，单位为 px。<br />**默认值：** 0 |
| items | Array[{title, description, icon, activeIcon, size}] | true | 步骤详情。<br />**默认值：** [] |
| showStepNumber | Boolean | false | 是否以数字序列展示步骤 icon。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.1.2](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| horizHighlight | Boolean | false | 用于控制水平方向是否启用高亮展示 title。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.1.3](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| iconFail | String | false | 设置失败步骤的 icon 类型。<br />**可选值：** 参考 [am-icon](https://opendocs.alipay.com/mini/component-ext/am-icon) 的 type 值<br />**默认值：** close<br />**版本要求：** mini-ali-ui [1.1.7](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| iconSuccess | String | false | 设置已激活步骤的 icon 类型。<br />**可选值：** 参考 [am-icon](https://opendocs.alipay.com/mini/component-ext/am-icon) 的 type 值<br />**默认值：** check<br />**版本要求：** mini-ali-ui [1.1.7](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| iconSuccessBg | String | false | 当前激活步骤的 icon 背景色。<br />**可选值：** 参考 CSS 中的颜色值描述方式<br />**版本要求：** mini-ali-ui [1.1.7](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| iconSuccessColor | String | false | 当前激活步骤的 icon 文本颜色。<br />**可选值：** 参考 CSS 中的颜色值描述方式<br />**版本要求：** mini-ali-ui [1.1.7](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |

### slot

steps 组件中的 slot 插槽可根据具体的步骤数设置，如有 4 个步骤点，那么可插入 4 个 slot。

slot 名称的格式为：`desc_1`、`desc_2`、`desc_n`...以此类推，将 n 修改为指定 items 的序列即可。如下列代码将会第 4 个 items 中没有 description 值的时候显示 slot 内容。为了满足需求，当 title 部分没有值时，也可以通过类似方式插入 slot 内容。水平方向与垂直方向的 steps 组件都可以使用这两个 slot。

```html
<view slot="title_2" style="color: green; font-weight: bold;"
  >titile 的内容</view
>
<view slot="desc_4"
  >当前 item 没有 <text style="color: green;">description</text> 时，使用 slot
  内容。</view
>
```

> 下表中的 n 代表从 1 开始累加的数字

| **slotName** | **说明**                           |
| ------------ | ---------------------------------- |
| desc_n       | 当无 description 值时可展示的 slot |
| title_n      | 当无 title 值时可展示的 slot       |

### items

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| items.title | String | true | 步骤详情标题。 |
| items.description | String | true | 步骤详情描述。 |
| items.icon | String | true | 尚未到达步骤的 icon（只在 vertical 模式下生效）。 |
| items.activeIcon | String | true | 已到达步骤的 icon（只在 vertical 模式下生效）。 |
| items.size | Number | true | 已到达步骤 icon 的图标大小，单位为 px（只在 vertical 模式下生效）。 |

## Bug & Tip

- 当 `showStepNumber` 为 true 时将会忽略 items 属性中 icon 相关属性，仅以数字序列方式展示。
- slot 中的数字与 items 的序列相对应，将会在 items 属性中没有 description 时展示。
- `iconSuccessBg` 改变的不仅仅是当前已激活的步骤背景色，同时也将会修改线条颜色；如果 `items.activeIcon` 所使用的图片是含有透明背景的图片时，背景颜色也将会显示。
- 当使用的 icon 非图片形式时，`iconSuccessColor` 可修改 icon 的颜色以及数字序列的数字文本颜色。
- `iconSuccessBg` 和 `iconSuccessColor` 仅修改当前已激活的步骤，尚未达到的步骤保持灰色模式，且不可配置。
- 步骤中失败的提示仅提供修改 icon 类型，无修改颜色的配置。
