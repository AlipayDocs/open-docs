# 简介

列表将数据呈现为可以分为平铺和分组形式。使用列表以清单的形式干净，高效地显示大量或少量信息。一般来说，列表是基于文本内容的理想选择，也可以在列表中加入图标、按钮、箭头等其他元素扩展场景。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*4q61RJSr6m4AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=JVlQE2VGLHmBy7Lm0u4fegAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-list?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .axml 示例代码

```html
<view class="dyt-list" style="position: relative;">
  <scroll-view
    style="height: 100vh;"
    scroll-y
    onScrollToLower="onScrollToLower"
    enable-back-to-top="true"
  >
    <list>
      <view slot="header"> 列表头部 </view>
      <block a:for="{{items}}">
        <list-item
          a:if="{{item.actionType==='switch'}}"
          thumb="{{thumbUrl}}"
          index="{{index}}"
          onClick="onSwitchClick"
          value="{{switchValues[index]}}"
          key="items-{{index}}"
          lineTouchable="{{item.lineTouchable}}"
          briefx="简要信息"
          upperSubtitle="{{item.brief}}"
          last="{{index === (items.length - 1)}}"
        >
          {{item.title}}
          <am-switch slot="extra" checked="{{changeSwitch}}" />
        </list-item>
        <list-item
          a:elif="{{item.actionType ==='check'}}"
          thumb="{{thumbUrl}}"
          index="{{index}}"
          onClick="onCheckClick"
          value="{{checkValues[index]}}"
          key="items-{{index}}"
          last="{{index === (items.length - 1)}}"
        >
          {{item.title}}
          <am-radio slot="extra" checked="{{changeCheckbox}}" />
        </list-item>
        <list-item
          a:elif="{{item.actionType ==='capsule'}}"
          thumb="{{thumbUrl}}"
          index="{{index}}"
          onClick="onCapsuleClick"
          capsuleContent="{{item.capsuleContent}}"
          key="items-{{index}}"
          last="{{index === (items.length - 1)}}"
        >
          {{item.title}}
          <button slot="extra" type="ghost" shape="capsule">胶囊按钮</button>
        </list-item>
        <list-item
          a:else
          thumbx="{{thumb}}"
          arrow="{{item.arrow}}"
          align="{{item.align}}"
          index="{{index}}"
          onClick="onItemClick"
          key="items-{{index}}"
          enforceExtra="{{item.enforceExtra}}"
          title="{{item.title}}"
          titlePosition="middle"
          last="{{index === (items.length - 1)}}"
        >
          {{item.title}}
          <text slot="extra">{{item.extra}}</text>
        </list-item>
      </block>
      <view slot="footer"> 列表尾部 </view>
    </list>
    <list>
      <view slot="header"> 列表头部 </view>
      <block a:for="{{items2}}">
        <list-item
          thumb="{{item.thumb}}"
          arrow="{{item.arrow}}"
          onClick="onItemClick"
          index="items2-{{index}}"
          key="items2-{{index}}"
          data-filed="aaa"
          title="{{item.title}}"
          upperSubtitle="{{item.brief}}"
          last="{{index === (items2.length - 1)}}"
        >
          {{item.title}}
          <view a:if="{{item.extra}}" slot="extra"> {{item.extra}} </view>
        </list-item>
      </block>
      <view slot="footer"> 列表尾部 </view>
    </list>
    <list>
      <view slot="header"> 列表头部 </view>
      <block a:for="{{items3}}">
        <list-item
          thumb="{{item.thumb}}"
          arrow="{{item.arrow}}"
          index="items3-{{index}}"
          onClick="onItemClick"
          key="items3-{{index}}"
          last="{{index === (items3.length - 1)}}"
          upperSubtitle="{{item.brief}}"
          multipleLine="{{true}}"
        >
          {{item.title}}
          <view a:if="{{item.extra}}" slot="extra"> {{item.extra}} </view>
        </list-item>
      </block>
      <view slot="footer"> 列表尾部 </view>
    </list>
    <list>
      <view slot="header"> 列表头部 </view>
      <block a:for="{{items4}}">
        <list-item
          thumb="{{item.thumb}}"
          arrow="{{item.arrow}}"
          onClick="onItemClick"
          index="items4-{{index}}"
          last="{{index === (items4.length - 1)}}"
          key="items4-{{index}}"
          upperSubtitle="{{item.upperSubtitle}}"
          lowerSubtitle="{{item.upperSubtitle}}"
          titlePosition="{{item.titlePosition}}"
        >
          {{item.title}}
          <view a:if="{{item.extra}}" slot="extra"> {{item.extra}} </view>
        </list-item>
      </block>
      <view slot="footer"> 列表尾部 </view>
    </list>
    <list>
      <view slot="header"> 小图文列表 </view>
      <block a:for="{{itemsThumb}}">
        <list-item
          thumb="{{item.thumb}}"
          arrow="{{item.arrow}}"
          onClick="onItemClick"
          index="itemsThumb-{{index}}"
          last="{{index === (itemsThumb.length - 1)}}"
          brief="{{item.brief}}"
          key="itemsThumb-{{index}}"
        >
          {{item.title}}
          <view a:if="{{item.extra}}" slot="extra"> {{item.extra}} </view>
        </list-item>
      </block>
    </list>
    <list>
      <view slot="header"> 小图文双行列表 </view>
      <block a:for="{{itemsThumbMultiple}}">
        <list-item
          thumb="{{item.thumb}}"
          arrow="{{item.arrow}}"
          onClick="onItemClick"
          index="items-multiple-{{index}}"
          last="{{index === (itemsThumbMultiple.length - 1)}}"
          key="items-multiple-{{index}}"
          upperSubtitle="{{item.brief}}"
          multipleLineX="{{true}}"
        >
          {{item.title}}
          <view a:if="{{item.extra}}" slot="extra"> {{item.extra}} </view>
        </list-item>
      </block>
    </list>
    <list loadMore="{{loadMore}}" loadContent="{{loadContent}}">
      <view slot="header"> 无限滚动列表 </view>
      <block a:for="{{items5}}">
        <list-item
          className="{{item.sticky ? 'am-list-sticky' : ''}}"
          thumb="{{item.thumb}}"
          arrow="{{item.arrow}}"
          align="{{item.align}}"
          last="{{index === (items5.length - 1)}}"
          index="{{index}}"
          key="items5-{{index}}"
          onClick="onItemClick"
          disabled="{{item.sticky}}"
          wrap="{{true}}"
        >
          {{item.title}}{{index}}
          <view a:if="{{item.extra}}" slot="extra"> {{item.extra}} </view>
        </list-item>
      </block>
    </list>
  </scroll-view>
</view>
```

### .js 示例代码

```javascript
// const imgUrl = '';
const newitems = [
  {
    thumb:
      'https://gw.alipayobjects.com/zos/rmsportal/KXDIRejMrRdKlSEcLseB.png',
    title: '固定到头部',
    arrow: true,
    sticky: true,
  },
  {
    title: '标题文字不换行很长很长很长很长很长很长很长很长很长很长',
    arrow: true,
  },
  {
    title: '标题文字换行很长很长很长很长很长很长很长很长很长很长',
    arrow: true,
    textMode: 'wrap',
  },
  {
    title: '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
    extra: '没有箭头',
    textMode: 'wrap',
  },
  {
    title: '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
    extra: '子元素垂直对齐',
    textMode: 'wrap',
    align: 'top',
  },
  {
    title: '标题文字换行很长很长很长很长很长很长很长很长很长很长',
    arrow: true,
    textMode: 'wrap',
  },
  {
    title: '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
    extra: '没有箭头',
    textMode: 'wrap',
  },
  {
    title: '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
    extra: '子元素垂直对齐',
    textMode: 'wrap',
    align: 'top',
  },
  {
    title: '标题文字换行很长很长很长很长很长很长很长很长很长很长',
    arrow: true,
    textMode: 'wrap',
  },
  {
    title: '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
    extra: '没有箭头',
    textMode: 'wrap',
  },
  {
    title: '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
    extra: '子元素垂直对齐',
    textMode: 'wrap',
    align: 'top',
  },
  {
    title: '标题文字换行很长很长很长很长很长很长很长很长很长很长',
    arrow: true,
    textMode: 'wrap',
  },
  {
    title: '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
    extra: '没有箭头',
    textMode: 'wrap',
  },
  {
    title: '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
    extra: '子元素垂直对齐',
    textMode: 'wrap',
    align: 'top',
  },
];
Page({
  data: {
    items: [
      {
        title: '单行列表1',
        extra: '详细信息',
        arrow: true,
      },
      {
        title: '单行列表2',
        extra: '+20.08',
        arrow: true,
        enforceExtra: true,
      },
      {
        title: '单行开关3',
        actionType: 'switch',
        index: 'switch',
        lineTouchable: false,
      },
      {
        title: '单行选项4',
        actionType: 'check',
        // actionValue: false,
        index: 'check',
      },
      {
        title: '单行列表5',
        actionType: 'capsule',
        capsuleContent: '胶囊按钮',
      },
    ],
    items2: [
      {
        title: '列表组',
        arrow: true,
      },
      {
        title: '列表组',
      },
      {
        title: '列表组',
      },
      {
        title: '列表组',
      },
      {
        title: '列表组',
      },
    ],
    items3: [
      {
        title: '双行列表',
        brief: '描述信息',
        arrow: true,
      },
    ],
    items4: [
      {
        title: '三行列表',
        upperSubtitle: '上副标题',
        lowerSubtitle: '下副标题',
        titlePosition: 'top',
        arrow: true,
      },
      {
        title: '三行列表',
        upperSubtitle: '上副标题',
        lowerSubtitle: '下副标题',
        titlePosition: 'middle',
        arrow: true,
      },
      {
        title: '三行列表',
        upperSubtitle: '上副标题',
        lowerSubtitle: '下副标题',
        titlePosition: 'bottom',
        arrow: true,
      },
    ],
    itemsThumb: [
      {
        thumb: 'https://tfsimg.alipay.com/images/partner/T12rhxXkxcXXXXXXXX',
        title: '标题文字',
        extra: '描述文字',
        arrow: true,
      },
      {
        thumb: 'https://tfsimg.alipay.com/images/partner/T12rhxXkxcXXXXXXXX',
        title: '标题文字',
        arrow: true,
      },
      {
        thumb: 'https://tfsimg.alipay.com/images/partner/T12rhxXkxcXXXXXXXX',
        title: '标题文字',
        arrow: true,
      },
    ],
    itemsThumbMultiple: [
      {
        thumb: 'https://tfsimg.alipay.com/images/partner/T12rhxXkxcXXXXXXXX',
        title: '标题文字',
        brief: '描述信息',
        arrow: true,
      },
      {
        thumb: 'https://tfsimg.alipay.com/images/partner/T12rhxXkxcXXXXXXXX',
        title: '标题文字',
      },
      {
        thumb: 'https://tfsimg.alipay.com/images/partner/T12rhxXkxcXXXXXXXX',
        title: '标题文字',
      },
    ],
    items5: [
      {
        thumb:
          'https://gw.alipayobjects.com/zos/rmsportal/KXDIRejMrRdKlSEcLseB.png',
        title: '固定到头部',
        brief: '描述信息',
        arrow: true,
        sticky: true,
      },
      {
        title: '标题文字不换行很长很长很长很长很长很长很长很长很长很长',
        arrow: true,
        align: 'middle',
      },
      {
        title: '标题文字换行很长很长很长很长很长很长很长很长很长很长',
        arrow: true,
        align: 'top',
      },
      {
        title:
          '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
        extra: '没有箭头',
        align: 'bottom',
      },
      {
        title:
          '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
        extra: '子元素垂直对齐',
        align: 'top',
      },
      {
        title: '标题文字换行很长很长很长很长很长很长很长很长很长很长',
        arrow: true,
      },
      {
        title:
          '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
        extra: '没有箭头',
      },
      {
        title:
          '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
        extra: '子元素垂直对齐',
        align: 'top',
      },
      {
        title: '标题文字换行很长很长很长很长很长很长很长很长很长很长',
        arrow: true,
      },
      {
        title:
          '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
        extra: '没有箭头',
      },
      {
        title:
          '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
        extra: '子元素垂直对齐',
        align: 'top',
      },
      {
        title: '标题文字换行很长很长很长很长很长很长很长很长很长很长',
        arrow: true,
      },
      {
        title:
          '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
        extra: '没有箭头',
      },
      {
        title:
          '标题文字很长很长很长很长很长很长很长很长很长很长很长很长很长很长',
        extra: '子元素垂直对齐',
        align: 'middle',
      },
    ],
    loadMore: '',
    maxList: 5,
    switchValues: {
      // switch: true,
      // check: false,
    },
    checkValues: {},
    thumb:
      'https://gw-office.alipayobjects.com/basement_prod/47775269-5c8e-40b8-bcda-43380022f311.jpg',
    changeCheckbox: true,
    changeSwitch: true,
  },
  onLoad() {
    const charCode = 65;
    const charList = [];
    for (let i = 0; i < 26; i++) {
      charList.push(String.fromCharCode(charCode + i));
    }
    this.setData({
      alphabet: charList,
    });
  },
  onItemClick(ev) {
    if (ev.detail && ev.index === 'check') {
      this.setData({
        actionValues: {
          ...this.data.actionValues,
          [ev.index]: ev.detail.value,
        },
      });
    } else {
      my.alert({
        content: `点击了第${ev.index}行`,
      });
    }
  },
  onSwitchClick() {
    this.setData({
      changeSwitch: !this.data.changeSwitch,
    });
    my.alert({
      content: 'switch changed',
    });
  },
  onCheckClick() {
    this.setData({
      changeCheckbox: !this.data.changeCheckbox,
    });
    my.alert({
      content: 'checkbox changed',
    });
  },
  onCapsuleClick() {
    my.alert({
      content: 'capsule button click',
    });
  },
  onScrollToLower() {
    this.setData({
      loadMore: 'load',
    });
    const { items5 } = this.data;
    // 加入 maxList 用于判断“假设”数据加载完毕后的情况
    if (this.data.maxList > 0) {
      const newItems = items5.concat(newitems);
      const MAXList = this.data.maxList - 1;
      this.setData({
        items5: newItems,
        maxList: MAXList,
      });
    } else {
      // 数据加载完毕之后，改变 loadMore 为 over 即可
      this.setData({
        loadMore: 'over',
      });
    }
  },
  onAlphabetClick(ev) {
    my.alert({
      content: JSON.stringify(ev.data),
    });
  },
});
```

### .json 示例代码

```json
{
  "defaultTitle": "List",
  "usingComponents": {
    "list": "mini-ali-ui/es/list/index",
    "list-item": "mini-ali-ui/es/list/list-item/index",
    "alphabet": "mini-ali-ui/es/list/alphabet/index",
    "list-secondary": "mini-ali-ui/es/list/list-secondary/index",
    "tag": "mini-ali-ui/es/tag/index",
    "am-icon": "mini-ali-ui/es/am-icon/index",
    "am-switch": "mini-ali-ui/es/am-switch/index",
    "am-radio": "mini-ali-ui/es/am-radio/index",
    "button": "mini-ali-ui/es/button/index"
  }
}
```

### .acss 示例代码

```css
.dyt-list {
  margin-top: 0;
}
.dyt-list .am-list-item-thumb {
  border-radius: 5px;
}
.dyt-list .am-list-briefX {
  color: #909090;
  font-size: 14px;
}
.am-list-sticky {
  position: sticky;
  top: 0;
  z-index: 2;
}
.am-list-item .a-icon-success_no_circle {
  fill: #1677ff;
}
.am-list-item .a-shared-checkbox {
  border: 0;
}
```

## 属性

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| loadMore | String | 显示加载更多 item。<br /><li>load：显示加载更多</li><li>over：显示加载完成无更多</li> |
| loadContent | Array | 需结合 loadMore 属性使用，用于文案展示。<br />**默认值：** ['加载更多...','-- 数据加载完了 --'] |
| loadingSize | String | loading icon 的大小。<br />**默认值：** 16 px |

### loadMore 使用介绍

当需要使用无限循环列表时，可将 list 组件放置入到 [scroll-view](https://opendocs.alipay.com/mini/component/scroll-view) 中，根据需求对 [scroll-view](https://opendocs.alipay.com/mini/component/scroll-view) 添加相对应的属性，比如：

```xml
<scroll-view style="height: 80vh;" scroll-y onScrollToLower="onScrollToLower" enable-back-to-top="true">
 <list loadMore="{{loadMore}}" loadContent="{{loadContent}}">
   <list-item>...</list-item>
 </list>
</scroll-view>
```

```javascript
Page({
  data: {
    loadMore: '',
    loadContent: ['马不停蹄加载更多数据中...', '-- 已经到底了，加不了咯 --'],
  },
  onScrollToLower() {
    // 根据实际数据加载情况设定 loadMore 的值即可，分别为 load 和 over
    this.setData({
      loadMore: 'load',
    });
  },
});
```

### slots

| **slotName** | **描述**                 |
| ------------ | ------------------------ |
| header       | 可选，列表头部。         |
| footer       | 可选，用于渲染列表尾部。 |
