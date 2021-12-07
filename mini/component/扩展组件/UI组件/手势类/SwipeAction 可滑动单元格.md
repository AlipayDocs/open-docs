
# 简介
可滑动单元格。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*mFvzSLKvHNkAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=RSHzP1ClIiW9jF9s9JrMZQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-swipe-action?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "Swipe-action",
  "usingComponents": {
    "list": "mini-ali-ui/es/list/index",
    "list-item": "mini-ali-ui/es/list/list-item/index",
    "swipe-action": "mini-ali-ui/es/swipe-action/index"
  }
}
```

### .axml 示例代码
```html
<view>
	<list>
		<view a:for="{{list}}" key="{{item.content}}">
			<swipe-action
				index="{{index}}"
				restore="{{swipeIndex === null || swipeIndex !== index}}"
				right="{{item.right}}"
				onRightItemClick="onRightItemClick"
				onSwipeStart="onSwipeStart"
				extra="item{{index}}"
				borderRadius="{{index <= 2 ? true : false}}"
			>
				<list-item
					arrow="horizontal"
					index="{{index}}"
					key="items-{{index}}"
					onClick="onItemClick"
					last="{{index === list.length - 1}}"
					upperSubtitle="{{index >= 4?'这是一个有副标题的列表':''}}"
					lowerSubtitle="{{index === 5?'这是一个小的副标题':''}}"
					borderRadius="{{index <= 2 ? true : false}}"
				>
					{{item.content}}
				</list-item>
			</swipe-action>
		</view>
	</list>
</view>
```

### .js 示例代码
```java
Page({
  data: {
    swipeIndex: null,
    list: [
      { right: [{ type: 'delete', text: '删除', fColor: 'black' }], content: '更换文字颜色' },
      { right: [{ type: 'edit', text: '取消收藏', fColor: 'rgba(0,0,0,.5)' }, { type: 'delete', text: '删除', fColor: 'yellow' }, { type: 'other', text: '新增一个' }], content: '改变文字颜色' },
      { right: [{ type: 'edit', text: '取消收藏', bgColor: '#333' }, { type: 'delete', text: '删除' }], content: '其中一个背景色变化' },
      { right: [{ type: 'edit', text: '取消收藏', bgColor: '#ccc', fColor: '#f00' }, { type: 'delete', text: '删除', bgColor: '#0ff', fColor: '#333' }], content: '文字和背景色同时改变' },
      { right: [{ type: 'edit', text: '取消收藏取消收藏取消' }, { type: 'delete', text: '删除删除删除删除' }], content: '默认颜色样式' },
      { right: [{ type: 'edit', text: '取消关注' }, { type: 'other', text: '免打扰' }, { type: 'delete', text: '删除' }], content: '三个选项的卡片' },
      { right: [{ type: 'edit', text: '取消关注' }, { type: 'other', text: '免打扰' }, { type: 'delete', text: '删除' }], content: '三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片三个选项的卡片' },
    ],
  },
  onRightItemClick(e) {
    const { type } = e.detail;
    my.confirm({
      title: '温馨提示',
      content: `${e.index}-${e.extra}-${JSON.stringify(e.detail)}`,
      confirmButtonText: '确定',
      cancelButtonText: '取消',
      success: (result) => {
        const { list } = this.data;
        if (result.confirm) {
          if (type === 'delete') {
            list.splice(this.data.swipeIndex, 1);
          }
          my.showToast({
            content: '确定 => 执行滑动删除还原',
          });
          e.done();
        } else {
          my.showToast({
            content: '取消 => 滑动删除状态保持不变',
          });
        }
      },
    });
  },
  onItemClick(e) {
    my.alert({
      content: `dada${e.index}`,
    });
  },
  onSwipeStart(e) {
    this.setData({
      swipeIndex: e.index,
    });
  },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| right | Array | 滑动选项，最多三项。 |
| onRightItemClick | EventHandle | 右侧滑开后的元素点击事件。<br />**默认值：** ({index, detail, extra, done}) => void |
| onSwipeStart | EventHandle | 开始滑动的回调。<br />**默认值：** ({index}) => void |
| extra | String | 附属信息，会在 onRightItemClick 回调中获取。 |
| restore | Boolean | 还原组件到初始状态。<br />**默认值：** false |
| borderRadius | Boolean | 右侧 item 是否为圆角。<br />**默认值：** false |
| enableNew | Boolean | 使用 [moveable-area ](https://opendocs.alipay.com/mini/component/movable-area)实现的 swipe-action。<br />**默认值：** true |
| swipeWidth | String | 设置 swipe-action 组件的宽度。默认为 my.getSystemInfoSync() 所得的 windowWidth，传入的宽度值不接受百分比单位，建议使用 px 或者 rpx。<br />**版本要求：** mini-ali-ui [1.0.10](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |


## Bug & Tip

- 当有多个 SwipeAction 组件时，当滑动其中一个时，需要将其他的组件的 `restore` 属性设置为 true，避免一个页面同时存在多个 swipeAction 处于活动状态。
- `right` 数组中的格式：[{ type: '', text: '', fColor: '', bgColor: '',},]。  
- `right` 中的 type 共有三个值：edit、delete 和 other。
- `fColor` 为文本颜色，`bgColor` 为背景色颜色，三种 type 均可自定义颜色，如未设置，默认值为：
   - edit：#ccc
   - delete：#FF3B30
   - other：#1677FF
- SwipeAction 是与 list 组件组合使用的。
- `borderRadius `是为了结合带圆角的 list-item 而存在的，如果为 true 时，将会把右侧 item 显示为圆角模式。
- `swipeWidth` 可设置 swipe-action 组件的整体宽度，默认为 `my.getSystemInfoSync()` 所得的 `windowWidth`，传入的宽度值不接受百分比单位，建议使用 `px` 或者 `rpx`。
- 如列表数据过多有卡顿情况，建议将 enableNew 设置为 false。
