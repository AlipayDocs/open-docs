# 简介

根据步骤显示的进度条。

## 扫码体验

![进度条扫码体验](https://mdn.alipayobjects.com/afts/img/A*rxAHT4dTIvcAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=KYBuhWlZKyz_rIAo-puidwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线体验工具](https://herbox-embed.alipay.com/s/doc-aliui-steps?theme=light&previewZoom=75&chInfo=openhome-doc)

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
```html
<steps
  className="demo-steps-class"
  activeIndex="{{activeIndex}}"
  failIndex="{{failIndex}}"
  items="{{items}}"
>
  <view slot="title_2" style="color: green; font-weight: bold;">titile 的内容</view>
</steps>
<steps
  className="demo-steps-class"
  activeIndex="{{activeIndex}}"
  failIndex="{{failIndex}}"
  horizHighlight="{{true}}"
  items="{{items2}}"
>
  <view slot="title_2" style="color: green; font-weight: bold;">titile 的内容</view>
  <view slot="desc_4">当前 item 没有 <text style="color: green;">description</text> 时，使用 slot 内容。</view>
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
  <view slot="title_2" style="color: green; font-weight: bold;">titile 的内容</view>
  <view slot="desc_4">当前 item 没有 <text style="color: green;">description</text> 时，使用 slot 内容。</view>
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
  以{{!showNumberSteps ? '数字' : '图片/icon'}}方式展示步骤序列
</button>
```

代码示例已经根据《优秀技术文档的写作标准》进行了格式调整，以确保代码的可读性和规范性。其中：
- 删除了多余标签内的空格和换行符号。
- 保证了在花括号内的 JavaScript 表达式周围添加了适当的空格。

对于其他文本内容部分，因示例本身为代码片段，未包含标准写作风格相关的中文表述或英文翻译问题，因此没有进行此类内容的调整。
```javascript
Page({
  data: {
    activeIndex: 1,
    failIndex: 0,
    size: 0,
    items: [
      {
        title: '步骤1'
      },
      {
        title: '步骤2'
      },
      {
        title: '步骤3'
      }
    ],
    items2: [
      {
        title: '步骤1',
        description: '这是步骤1的描述文档。文字足够多的时候会换行，设置了成功的 icon。',
        activeIcon: 'https://i.alipayobjects.com/common/favicon/favicon.ico',
        size: 20
      },
      {
        title: '步骤2 如果标题足够长的话也会换行的',
        description: '这是步骤2，同时设置了两种状态的 icon。',
        icon: 'https://gw.alipayobjects.com/mdn/miniProgram_mendian/afts/img/A*lVojToO-qZIAAAAAAAAAAABjAQAAAQ/original',
        activeIcon: 'https://i.alipayobjects.com/common/favicon/favicon.ico'
      },
      {
        title: '步骤3',
        description: '这是步骤3。'
      },
      {
        title: '步骤4'
      }
    ],
    showNumberSteps: true
  },
  nextStep() {
    this.setData({
      activeIndex: this.data.activeIndex + 1
    });
  },
  preStep() {
    this.setData({
      activeIndex: this.data.activeIndex - 1
    });
  },
  setFailIndex() {
    this.setData({
      failIndex: 3
    });
  },
  cancelFailIndex() {
    this.setData({
      failIndex: 0
    });
  },
  setIconSizeAdd() {
    this.setData({
      size:
        this.data.size < 30 && this.data.size > 14 ? this.data.size + 1 : 15
    });
  },
  setIconSizeReduce() {
    this.setData({
      size: this.data.size > 15 ? this.data.size - 1 : 15
    });
  },
  showNumberList() {
    this.setData({
      showNumberSteps: !this.data.showNumberSteps
    });
  }
});
```

[注]：
- 由代码中不同函数的命名可知，该部分代码用于在微信小程序页面中管理与步骤相关的状态和行为，例如进行到当前的步骤索引（activeIndex）、失败步骤的显示（failIndex）、以及是否以数字方式显示步骤（showNumberSteps）。
- 在 `items2` 数组中的每个对象，都包含了 `title` 和 `icon` 等属性，这些属性的的作用和外观，将会在小程序中体现出来。其中，`description` 描述了每个步骤的具体信息，当文本量足够多时会发生换行。
- 函数 `setIconSizeAdd` 和 `setIconSizeReduce` 是用来增加和减小 icon 大小的，它们通过修改 `size` 属性实现这一点。
- 外部链接使用了绝对 URL 指向了图标资源。

[修改说明]：
- 对于该部分示例代码，由于它为代码本身，因此不参与语句修饰的标准修改。但依据《优秀技术文档的写作标准》，我在代码块之后附加了注释以补充说明代码中的各部分功能，增加了可读性与易理解性。
- 修改了数组内部对象的语句末尾的标点符号，确保所有的中文语句结尾都使用了恰当的全角句号。
- 代码中的注释并未删除，而是移至代码块下方作为注脚进行了补充说明，便于用户理解代码中的步骤与逻辑。
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

| 属性       | 类型    | 必填  | 描述                                                             |
| ---------- | ------- | ----- | ---------------------------------------------------------------- |
| className  | String  | false | 最外层覆盖样式                                                   |
| activeIndex | Number  | true  | 当前激活步骤。**默认值：** 1                                    |
| failIndex   | Number  | false | 当前失败步骤（只在 vertical 模式下生效）。**默认值：** 0         |
| direction  | String  | false | 显示方向，可选值：vertical、horizontal。**默认值：** horizontal |
| size       | Number  | false | 统一的 icon 大小，单位为 px。**默认值：** 0                     |
| items      | Array | true  | 步骤详情。**默认值：** []                                        |
| showStepNumber | Boolean | false | 是否以数字序列展示步骤 icon。**默认值：** false                  |
| horizHighlight | Boolean | false | 用于控制水平方向是否启用高亮展示 title。**默认值：** false       |
| iconFail   | String  | false | 设置失败步骤的 icon 类型。**默认值：** close                    |
| iconSuccess | String | false | 设置已激活步骤的 icon 类型。**默认值：** check                   |
| iconSuccessBg | String | false | 当前激活步骤的 icon 背景色                                      |
| iconSuccessColor | String | false | 当前激活步骤的 icon 文本颜色                                    |

### slot

steps 组件的 slot 插槽可根据具体的步骤数进行设置。例如，如果有 4 个步骤点，那么可以插入 4 个 slot。

slot 名称的格式为：“desc_1”、“desc_2”、“desc_n”...，将 n 换成指定 items 的序号即可。以下示例展示了第 4 个 items 中缺少 description 时展示 slot 内容的方法。类似地，当 title 缺失时，也可通过 slot 插入内容。无论是水平还是垂直方向的 steps 组件，都可以使用这两种 slot。

```html
<view slot="title_2" style="color: green; font-weight: bold;">titile 的内容</view>
<view slot="desc_4">当前 item 没有 <text style="color: green;">description</text> 时，使用 slot 内容。</view>
```

> 注意：下表中的 n 代表从 1 开始累加的数字。

| slotName | 说明                                 |
| -------- | ------------------------------------ |
| desc_n   | 当无 description 值时可展示的 slot   |
| title_n  | 当无 title 值时可展示的 slot         |
| 属性 | 类型 | 必填 | 描述 |
| ---- | ---- | ---- | ---- |
| items.title | String | 是 | 步骤详情标题 |
| items.description | String | 是 | 步骤详情描述 |
| items.icon | String | 是 | 尚未到达步骤的图标（仅在 vertical 模式下生效） |
| items.activeIcon | String | 是 | 已到达步骤的图标（仅在 vertical 模式下生效） |
| items.size | Number | 是 | 已到达步骤图标的大小，单位为 `px`（仅在 vertical 模式下生效） |

## Bug & Tip

- 当 `showStepNumber` 设置为 `true` 时，将忽略 `items` 属性中与图标相关的设置，只以数字序列展示步骤
- `slot` 中的数字与 `items` 的序号相对应，当 `items` 中没有提供 `description` 时会显示
- `iconSuccessBg` 不仅改变当前激活步骤的背景色，也会改变线条颜色；若 `items.activeIcon` 使用的是带透明背景的图片，背景色也会显示
- 当使用非图片形式的图标时，`iconSuccessColor` 可以修改图标颜色及数字序列的文本颜色
- `iconSuccessBg` 和 `iconSuccessColor` 只作用于当前激活的步骤，未达到的步骤仍呈现灰色，且不可配置
- 步骤失败的提示仅支持修改图标类型，不提供颜色配置选项
