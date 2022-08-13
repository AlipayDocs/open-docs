# 简介
**my.optionsSelect** 用于唤起 select 选择器，支持单列选择和二级数据选择。

## 使用限制

- 不支持二级联动（如有此类需求请使用 [my.multiLevelSelect](https://opendocs.alipay.com/mini/api/multi-level-select)）。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/71fa9403bcebcd54e5c800bbde9f006b.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/options-select?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 


### .js 示例代码

```javascript
Page({
  openOne() {
    my.optionsSelect({
      title: "还款日选择",
      optionsOne: ["每周一", "每周二", "每周三", "每周四", "每周五", "每周六", "每周日"],
      selectedOneIndex: 2,
      success(res) {
        my.alert({
          content: JSON.stringify(res, null, 2),
        });
      }
    });
  },
  openTwo() {
    my.optionsSelect({
      title: "出生年月选择",
      optionsOne: ["2014年", "2013年", "2012年", "2011年", "2010年", "2009年", "2008年"],
      optionsTwo: ["一月", "二月", "三月", "四月", "五月", "六月", "七月", "八月", "九月", "十月", "十一月", "十二月"],
      selectedOneIndex: 3,
      selectedTwoIndex: 5,
      success(res) {
        my.alert({
          content: JSON.stringify(res, null, 2),
        });
      }
    });
  },
});
```

## 入参

入参为 Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 头部标题信息。 |
| optionsOne | String[] | 是 | 选项一列表。 |
| optionsTwo | String[] | 否 | 选项二列表。 |
| selectedOneIndex | Number | 否 | 选项一默认选中。默认值为 0。 |
| selectedTwoIndex | Number | 否 | 选项二默认选中。默认值为 0。 |
| positiveString | String | 否 | 确定按钮文案。默认为确定。 |
| negativeString | String | 否 | 取消按钮文档。默认为取消。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| selectedOneIndex | Number | 选项一选择的值。<br />若选择取消，则返回空字符串。 |
| selectedOneOption | String | 选项一选择的内容。<br />若选择取消，则返回空字符串。 |
| selectedTwoIndex | Number | 选项二选择的值。<br />若选择取消，则返回空字符串。 |
| selectedTwoOption | String | 选项二选择的内容。<br />若选择取消，则返回空字符串。 |

# 常见问题 FAQ
## Q：如何引用 json 文件作为选项列表参数数据？
A：可以先通过 [FileSystemManager.readFile](https://opendocs.alipay.com/mini/api/0226oj) 读取 json 文件内容，然后再调用 my.optionsSelect。

### .js 示例代码
```javascript
const fs = my.getFileSystemManager();
fs.readFile({
  filePath: '/pages/test.json',
  encoding: 'utf-8',
  success(res) {
    my.alert({
      content: JSON.stringify(JSON.stringify(res.data))
    });
    
    const json = JSON.parse(res.data);
    console.log(json)
    
    my.optionsSelect({
      title: "还款日选择",
      optionsOne: json.year,
      selectedOneIndex: 2,
      success(res) {
        my.alert({
          content: JSON.stringify(res, null, 2)
        });
      }
    });
  },
  fail(res) {
    my.alert({
      content: JSON.stringify(res)
    });
  },
})

