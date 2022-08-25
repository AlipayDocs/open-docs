# 简介

单日历组件。不支持跨页选择日期范围。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*QTU7SIUZWwkAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=p-804BKLyQGDJy97jUCirwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-calendar?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Calendar",
  "usingComponents": {
    "calendar": "mini-ali-ui/es/calendar/index"
  }
}
```

### .axml 示例代码

```html
<view>
  <calendar
    type="range"
    haveYear="{{true}}"
    tagData="{{tagData}}"
    onSelect="handleSelect"
    onMonthChange="onMonthChange"
    onYearChange="onYearChange"
    onChange="onChange"
    onSelectHasDisableDate="onSelectHasDisableDate"
  />
</view>
```

### .js 示例代码

```javascript
Page({
  data: {
    tagData: [
      { date: '2020-02-14', tag: '颜色 1', tagColor: 1 },
      { date: '2020-02-28', tag: '公积金', tagColor: 2 },
      { date: '2020-02-24', tag: '颜色 3', tagColor: 3 },
      { date: '2020-02-18', tag: '颜色 4', tagColor: 4 },
      { date: '2020-02-4', tag: '还房贷', tagColor: 5 },
      { date: '2020-02-10', tag: '公积金', disable: true },
    ],
  },
  handleSelect() {},
  onMonthChange() {},
  onYearChange() {},
  onChange() {},
  onSelectHasDisableDate() {
    my.alert({
      content: 'SelectHasDisableDate',
    });
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| type | String | 选择类型。<br />**可选值：** <br />single: 单日 <br />range: 日期区间<br />**默认值：** single |
| haveYear | Boolean | 是否展示年份控制箭头。<br />**默认值：** false |
| prevMonthDisable | Boolean | 前一个月份箭头禁用。<br />**默认值：** false |
| prevYearDisable | Boolean | 前一个年份箭头禁用。<br />**默认值：** false |
| nextvMonthDisable | Boolean | 后一个月份箭头禁用。<br />**默认值：** false |
| nextYearDisable | Boolean | 后一个年份箭头禁用。<br />**默认值：** false |
| tagData | Array | [{ date: '日期', tag: '标签', tagColor: 1, disable: true,},]，可设置多个不同日期的标签内容，颜色以及是否禁用。 |
| onSelect | EventHandle | 选择区间时的回调。<br />**默认值：** ([startDate, endDate]) => void |
| onMonthChange | EventHandle | 点击切换月份时回调，带两个参数 currentMonth 切换后月份和 prevMonth 切换前月份。<br />**默认值：** (currentMonth, prevMonth) => void |
| onChange | EventHandle | 年/月变化时回调，带两个对象，每个均携带 year 和 month 信息。<br />**默认值：** (current, prev) => void<br />**版本要求：** mini-ali-ui [1.1.5](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| onSelectHasDisableDate | EventHandle | 选择区间包含不可用日期。<br />**默认值：** (currentMonth, prevMonth) => void |
| onYearChange | EventHandle | 点击切换年份时回调，带两个参数 currentYear 切换后年份和 prevYear 切换前年份。<br />**默认值：** (currentYear, prevYear) => void |

## Bug & Tip

- tagColor 共有 5 种颜色：
  - 1: #ff6010
  - 2: #00b578
  - 3: #ff8f1f
  - 4: #1677ff
  - 5: #999
- prevMonthDisable、prevYearDisable、nextvMonthDisable 以及 nextYearDisable 四个主要控制日历上的箭头是否可点击使用，可根据实际业务场景来使用。
- tagData 中的 disable 是可选项，如某日期需要提示禁用不可点时才需要增加，当不可用时，tag 以及 tagColor 将不会展示。
- 月份计数从 0 开始，即 0 代表 1 月份，以此类推，月份返回值 11 代表 12 月份。
