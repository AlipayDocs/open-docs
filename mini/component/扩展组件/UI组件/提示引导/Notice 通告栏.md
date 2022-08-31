# 简介

当应用有重要公告或者由于用户的刷新操作产生提示反馈时可以使用通告栏系统。通告栏不会对用户浏览当前页面内容产生影响，但又能明显的引起用户的注意。

## 使用限制

- 仅用于 UI 展示没有对应的业务逻辑功能。
- notice 为瀑布流布局不会定位到页面头部，用户可以根据需求将它放在相应位置。
- 当使用循环滚动功能时，公告字数不满一行无法滚动，只有内容超过一行后才可滚动。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*06nrQ59oMj4AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=Xqkh2vEWDnjXvk-6JX_3GwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-notice?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Notice",
  "usingComponents": {
    "notice": "mini-ali-ui/es/notice/index"
  }
}
```

### .axml 示例代码

```html
<notice
  marqueeProps="{{marqueeProps}}"
  enableMarquee="{{true}}"
  show="{{true}}"
  type="error"
  mode="link"
  onClick="actionClick"
  actionLeft="文字按钮"
  onClickLeft="linkActionClick"
>
  无限循环滚动的通告栏展示情况。文字不够继续添加文字凑数。
</notice>
<notice
  show="{{true}}"
  type="active"
  onClick="actionClick"
  capsule="{{true}}"
  capsuleItem="{{['https://img.alicdn.com/tfs/TB1yTvnfQY2gK0jSZFgXXc5OFXa-145-145.png','https://img.alicdn.com/tfs/TB1egTmfNz1gK0jSZSgXXavwpXa-145-145.png','https://img.alicdn.com/tfs/TB1l36mfQP2gK0jSZPxXXacQpXa-145-145.png','https://img.alicdn.com/tfs/TB1uCUdfND1gK0jSZFyXXciOVXa-151-164.png']}}"
  >4 个优惠信息推荐
</notice>
```

### .js 示例代码

```javascript
Page({
  data: {
    marqueeProps: {
      loop: true,
      leading: 1000,
      trailing: 800,
      fps: 40,
    },
  },
  linkActionClick() {
    my.showToast({
      content: '左侧操作区被点击了',
      duration: 1000,
    });
  },
  actionClick() {
    my.showToast({
      content: '你点击了右侧操作区',
      duration: 1000,
    });
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| mode | String | 右侧 icon 类型。<br />可选类型：<br /><li>link（以链接形式展示通告，默认以 > 表示）</li><li>closable（告知该通告可关闭，默认以 X 表示）</li> |
| action | String | 右侧文本按钮文案 |
| actionLeft | String | 右侧第二个按钮文案。 |
| onClick | EventHandle | 点击右侧按钮回调。<br />**默认值：** () => {} |
| onClickLeft | EventHandle | 点击右侧第二个按钮回调。<br />**默认值：** () => {} |
| show | Boolean | 是否显示 notice。<br />**默认值：** true |
| enableMarquee | Boolean | 是否开启动画。<br />**默认值：** false |
| marqueeProps | Object | marquee 参数。<br /><li>loop：是否循环</li><li>leading：动画开启前停顿</li><li>trailing：loop 为 true 时，动画间停顿。</li><li>fps：动画帧率</li><br/>**默认值：** {loop: false, leading: 500, trailing: 800, fps: 40 } |
| showIcon | Boolean | 是否显示 icon。<br />**默认值：** true |
| capsuleItem | Array | 胶囊通告栏的业务 logo url。 |
| capsule | Boolean | 是否为胶囊通告栏。<br />**默认值：** false |
| type | String | 通告栏类型。<br />**可选值：** normal、error、active、transparent。<br />**默认值：** normal |

## Bug & Tip

- 如果 `action` 没有任何值，那么 `actionLeft` 将不会显示。
- `onClick`、`onClickLeft` 相对应于 action 和 actionLeft。
- 当 `mode` 的值为 link，显示为一个箭头 icon 时，整条通告栏是可点击的。
- 当 `action` 有值时，将会代替 `mode` 中的 `closable` 和 link，只会显示文字。
- `capsuleItem` 在胶囊通告栏中只会显示 3 个，超过部分仅统计个数，但不会显示 logo。
- 当 `type` 的值为 `transparent` 时，展示的是带有透明度，内容色为白色的通告栏。
