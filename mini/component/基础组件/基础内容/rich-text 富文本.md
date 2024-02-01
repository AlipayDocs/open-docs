# 简介

富文本。

## 使用限制

- 版本要求基础库 1.11.0 及以上，若版本较低，建议进行[兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('rich-text')` 判断是否支持。
- 富文本里编写的 js 不支持事件执行。
- `rich-text` 支持 `a` 标签，不支持超链接。

## 扫码体验

![|127x157](https://cdn.nlark.com/yuque/0/2021/png/179989/1638425476338-51918621-16b6-4411-80b9-1c3996a659fc.png#align=left&display=inline&height=150&margin=%5Bobject%20Object%5D&name=image.png&originHeight=194&originWidth=157&size=16809&status=done&style=none&width=121)


# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/rich-text/index&defaultOpenedFiles=pages/rich-text/index&theme=light)

## 属性说明

| **属性**    | **类型**    | **描述**                                                                                                          |
|-------------|-------------|-------------------------------------------------------------------------------------------------------------------|
| `nodes`     | Array/String| 节点列表。基础库 [2.8.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持 `HTML String`，版本 [2.8.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 以下可使用 [mini-html-parser2](https://github.com/ant-mini-program/mini-html-parser) 将 `HTML String` 转化为 `nodes` 数组。 |
| `space`     | String      | 显示连续空格。**有效值**：<ul><li>`nbsp`：根据字体设置的空格大小。</li><li>`emsp`：中文字符空格大小。</li><li>`ensp`：中文字符空格一半大小。</li></ul>**版本要求**：基础库 [2.8.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上。 |
| `onTap`     | EventHandle | 触摸。                                                                                                            |
| `onTouchstart`| EventHandle| 触摸动作开始。                                                                                                    |
| `onTouchmove` | EventHandle| 触摸移动事件。                                                                                                    |
| `onTouchcancel`| EventHandle| 触摸动作被打断。                                                                                                  |
| `onTouchend`  | EventHandle| 触摸动作结束。                                                                                                    |
| `onLongtap`   | EventHandle| 触摸后，超过 500ms 再离开。                                                                                      |

### `nodes` 属性说明

现支持两种节点：元素节点和文本节点，通过 `type` 来区分。默认是元素节点，在富文本区域内显示的 HTML 节点。
#### 元素节点

| 属性 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| type | String | 否 | 节点类型，默认值：node |
| name | String | 是 | 标签名，支持部分受信任的 HTML 节点 |
| attrs | Object | 否 | 属性，支持部分受信任的属性，遵循 Pascal 命名法 |
| children | Array | 否 | 子节点列表，结构和 nodes 相同 |
| marks | Object | 否 | 可在 tap 和 longTap 事件中接收 |
**说明**：自基础库 2.7.1 起，在 tap 和 longTap 事件中，可以通过 event.detail.marks 获得从触发事件的节点到根节点上所有的 marks 合并结果。如果存在同名数据，子节点将覆盖父节点。

受信任的 HTML 节点及属性，支持 class 和 style 属性，不支持 id 属性。

| 节点 | 额外支持的属性 | 说明 |
| --- | --- | --- |
| a | - | - |
| abbr | - | - |
| address | - | 自基础库 2.7.4 起支持 |
| article | - | 自基础库 2.7.4 起支持 |
| aside | - | 自基础库 2.7.4 起支持 |
| b | - | - |
| bdr | - | 自基础库 2.7.4 起支持 |
| bdo | dir | 自基础库 2.7.4 起支持 |
| big | - | 自基础库 2.7.4 起支持 |
| blockquote | - | - |
| br | - | - |
| caption | - | 自基础库 2.7.4 起支持 |
| center | - | 自基础库 2.7.4 起支持 |
| cite | - | 自基础库 2.7.4 起支持 |
| code | - | - |
| col | span, width | - |
| colgroup | span, width | - |
| dd | - | - |
| del | - | - |
| div | - | - |
| dl | - | - |
| dt | - | - |
| em | - | - |
| fieldset | - | - |
| font | - | 自基础库 2.7.4 起支持 |
| footer | - | 自基础库 2.7.4 起支持 |
| h1 | - | - |
| h2 | - | - |
| h3 | - | - |
| h4 | - | - |
| h5 | - | - |
| h6 | - | - |
| header | - | 自基础库 2.7.4 起支持 |
| hr | - | - |
| i | - | - |
| img | alt, src, height, width | - |
| ins | - | - |
| label | - | - |
| legend | - | - |
| li | - | - |
| mark | - | 自基础库 2.7.4 起支持 |
| nav | - | 自基础库 2.7.4 起支持 |
| ol | start, type | - |
| p | - | - |
| pre | - | 自基础库 2.7.4 起支持 |
| q | - | - |
| rt | - | 自基础库 2.7.4 起支持 |
| ruby | - | 自基础库 2.7.4 起支持 |
| s | - | 自基础库 2.7.4 起支持 |
| section | - | 自基础库 2.7.4 起支持 |
| small | - | 自基础库 2.7.4 起支持 |
| span | - | 自基础库 2.7.4 起支持 |
| strong | - | - |
| sub | - | - |
| sup | - | - |
| table | width | - |
| tbody | - | - |
| td | colspan, height, rowspan, width | - |
| tfoot | - | - |
| th | colspan, height, rowspan, width | - |
| thead | - | - |
| tr | - | - |
| tt | - | 自基础库 2.7.4 起支持 |
| u | - | 自基础库 2.7.4 起支持 |
| ul | - | - |

仅支持如下字符实体，其他字符实体会导致组件无法渲染，而基础库 2.7.5 起始支持任意实体节点。

| 显示结果 | 描述 | 实体名称 |
| --- | --- | --- |
|   | 空格 | &nbsp; |
| < | 小于号 | &lt; |
| > | 大于号 | &gt; |
| & | 和号 | &amp; |
| " | 引号 | &quot; |
| ' | 撇号 | &apos; |
#### 文本节点

| 属性 | 类型   | 必填 | 描述                    |
| ---- | ------ | ---- | ----------------------- |
| type | String | 是   | 节点类型。`type` 为 `text` |
| text | String | 是   | 文本。                  |


# FAQ

### `rich-text` 富文本如何插入 html 包含标签的数据？

需要自己将 HTML 字符串转化为 nodes 数组。

### 如何处理 HTML 字符串中存在多个 `img` 标签且不闭合时，`mini-html-parser` 会转换错误？

`mini-html-parser2`（[链接](https://github.com/ant-mini-program/mini-html-parser)）0.3.0 已解决此问题。若当前使用老版本，请升级到最新的 0.3.0 版本即可。
### 如何为 rich-text 富文本添加链接跳转功能？

由于小程序的管控限制，rich-text 中的 a 标签无法像前端页面一样通过配置 `<a href="https://render.alipay.com/p/s/web-view/index">Webview Demo</a>` 来实现页面跳转。在小程序中，需要使用相应的 [JSAPI](https://opendocs.alipay.com/mini/api/yz6gnx) 或者 [路由 JSAPI](https://opendocs.alipay.com/mini/006l0z) 来实现跳转功能。

```javascript
// 使用上述 [mini-html-parser] 处理 HTML 字符串
import parse from 'mini-html-parser2';

const testHtmlString = '<a href="https://render.alipay.com/p/s/web-view/index">Webview Demo</a>';  // HTML 字符串
const HTML_A_TAG = 'a';  // 表示 a 标签的常量

Page({
  data: { nodes: [] },

  onLoad() {
    parse(testHtmlString, (err, nodes) => {
      if (!err) {
        const transferNodes = nodes.map(node => {
          const { children, name, attrs } = node;
          const obj = { ...node };
          // 在这里处理子节点（children）
          if (name === HTML_A_TAG) {
            // 如果是 a 标签，则将其 href 属性值保存到 marks 中，并移除 href 属性
            obj.marks = { ...attrs, name: HTML_A_TAG };
          }
          return obj;
        });
        this.setData({ nodes: transferNodes });  // 将处理后的节点更新到 rich-text 组件中
      } else {
        console.error('解析 HTML 出错: ', err);
      }
    });
  },

  handleOnTap(event) {
    const { marks } = event.detail;  // 从事件对象中获取自定义的 marks
    const { name, href } = marks || {};
    if (name === HTML_A_TAG && href) {
      // 如果是 a 标签，并且有对应的 href 属性值
      my.ap.navigateToAlipayPage({
        // 使用 my.navigateToMiniProgram 或其他跳转方法实际进行页面跳转
        path: href,
        success: () => {
          my.alert({ content: '跳转成功' });
        },
        fail: (error) => {
          my.alert({ content: '跳转失败：' + JSON.stringify(error) });
        },
      });
    }
  },
});
```

```html
<rich-text nodes="{{nodes}}" bindtap="handleOnTap"></rich-text>
```

即通过将跳转链接放置在节点的 marks 属性中，并通过 rich-text 组件的 onTap 事件来实现链接的跳转。
