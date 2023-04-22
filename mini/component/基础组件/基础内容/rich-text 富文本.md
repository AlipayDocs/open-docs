# 简介

富文本。

## 使用限制

- 版本要求基础库 1.11.0 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 富文本里面写 js 不支持事件执行。
- rich-text 支持 a 标签，不支持超链接。

## 扫码体验

![|127x157](https://cdn.nlark.com/yuque/0/2021/png/179989/1638425476338-51918621-16b6-4411-80b9-1c3996a659fc.png#align=left&display=inline&height=150&margin=%5Bobject%20Object%5D&name=image.png&originHeight=194&originWidth=157&size=16809&status=done&style=none&width=121)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/rich-text/index&defaultOpenedFiles=pages/rich-text/index&theme=light)

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| nodes | Array/String | 节点列表。基础库 [2.8.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持 HTML String，[2.8.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 以下版本可使用 [mini-html-parser2](https://github.com/ant-mini-program/mini-html-parser) 将 HTML String 转化为 nodes 数组。 |
| space | String | 显示连续空格。</br>**有效值**：<ul><li>nbsp：根据字体设置的空格大小。</li> <li>emsp：中文字符空格大小。</li> <li>ensp：中文字符空格一半大小。</li> </ul>**版本要求**：基础库 [2.8.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上。 |
| onTap | EventHandle | 触摸。 |
| onTouchstart | EventHandle | 触摸动作开始。 |
| onTouchmove | EventHandle | 触摸移动事件。 |
| onTouchcancel | EventHandle | 触摸动作被打断。 |
| onTouchend | EventHandle | 触摸动作结束。 |
| onLongtap | EventHandle | 触摸后，超过 500ms 再离开。 |

### nodes 属性

现支持两种节点：元素节点和文本节点，通过 type 来区分。默认是元素节点，在富文本区域里显示的 HTML 节点。<br />

#### 元素节点

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| type | String | 否 | 节点类型<br />默认值：node |
| name | String | 是 | 标签名。支持部分受信任的 HTML 节点。 |
| attrs | Object | 否 | 属性。支持部分受信任的属性，遵循 Pascal 命名法。 |
| children | Array | 否 | 子节点列表。结构和 nodes 相同。 |
| marks | Object | 否 | 可在 tap 和 longTap 事件中接收。<br /> **说明**：自基础库 [2.7.1](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起，在 tap 和 longTap 事件中，可以通过 event.detail.marks 获得从触发事件的节点到根节点上所有的 marks 合并结果。如果存在同名数据，子节点将覆盖父节点。<br /> |

受信任的 HTML 节点及属性。支持 class 和 style 属性，不支持 id 属性。

| **节点** | **额外支持的属性** | **说明** |
| --- | --- | --- |
| a | - | - |
| abbr | - | - |
| address | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| article | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| aside | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| b | - | - |
| bdr | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| bdo | dir | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| big | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| blockquote | - | - |
| br | - | - |
| caption | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| center | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| cite | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
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
| font | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| footer | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| h1 | - | - |
| h2 | - | - |
| h3 | - | - |
| h4 | - | - |
| h5 | - | - |
| h6 | - | - |
| header | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| hr | - | - |
| i | - | - |
| img | alt, src, height, width | - |
| ins | - | - |
| label | - | - |
| legend | - | - |
| li | - | - |
| mark | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| nav | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| ol | start, type | - |
| p | - | - |
| pre | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| q | - | - |
| rt | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| ruby | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| s | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| section | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| small | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| span | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
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
| tt | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| u | - | 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 起支持 |
| ul | - | - |

仅支持如下字符实体，其他字符实体会导致组件无法渲染。基础库 [2.7.5](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持任意实体节点。

| **显示结果** | **描述** | **实体名称** |
| ------------ | -------- | ------------ |
|              | 空格。   | &nbsp;       |
| <            | 小于号。 | &lt;         |
| >            | 大于号。 | &gt;         |
| &            | 和号。   | &amp;        |
| "            | 引号。   | &quot;       |
| '            | 撇号。   | &apos;       |

#### 文本节点

| **属性** | **类型** | **必填** | **描述**               |
| -------- | -------- | -------- | ---------------------- |
| type     | String   | 是       | 节点类型。type 为 text |
| text     | String   | 是       | 文本。                 |

# FAQ

### rich-text 富文本如何插入 html 包含标签的数据？

需要自己将 HTML String 转化为 nodes 数组。

### 如何处理 HTML String 中存在多个 img 标签且不闭合时，mini-html-parser 会转换错误？

[mini-html-parser2](https://github.com/ant-mini-program/mini-html-parser) 0.3.0 已解决此问题，若当前使用老版本，请升级到最新的 0.3.0 版本即可。

### 如何为 rich-text 富文本 添加链接跳转功能？

受小程序管控原因，rich-text 中的 a 标签，无法像前端页面中，配置 `<a href="https://render.alipay.com/p/s/web-view/index">Webview Demo</a>` 即可实现跳转；小程序中需要使用对应的 [JSAPI](https://opendocs.alipay.com/mini/api/yz6gnx) 或者 [路由 JSAPI](https://opendocs.alipay.com/mini/006l0z) 实现跳转路由。

```javascript
// 使用上述 [mini-html-parser] 处理 html 字符串
import parse from 'mini-html-parser2';

const testHtmlString =
  '<a href="https://render.alipay.com/p/s/web-view/index">Webview Demo</a>'; // html String
const HTML_A_TAG = 'a';

Page({
  data: { nodes: [] },

  onLoad() {
    parse(testHtmlString, (err, nodes) => {
      if (!err) {
        const transferNodes = nodes.map(i => {
          const { children, name, attrs } = i;
          const obj = i;
          // 这里没有处理 children
          if (name === HTML_A_TAG) {
            // 这里假定 原本的htmlstring中 a标签为原本跳转的元素
            obj.marks = { ...attrs, name: HTML_A_TAG }; // 小程序中不支持 a标签的href属性，先把对应的href 属性放在marks中
          }
          return obj;
        });
        this.setData({ nodes: transferNodes }); // 更新到 rich-text 组件上
      } else {
        console.log('err: ', err);
      }
    });
  },

  handleOnTap(e) {
    const {
      detail: { marks }, // 获取自定义的marks
    } = e;
    const { name, href } = marks || {}; //
    if (name === HTML_A_TAG && href) {
      // 判断是否是 a 标签，同时有 href 链接

      my.ap.navigateToAlipayPage({
        // 使用 my.navigateToMiniProgram 、my.navigateTo ... 实际跳转
        path: href,
        success: () => {
          my.alert({ content: '成功' });
        },
        fail: error => {
          my.alert({ content: '失败：' + JSON.stringify(error) });
        },
      });
    }
  },
});
```

```html
<rich-text nodes="{{nodes}}" onTap="handleOnTap"></rich-text>
```

即把跳转链接放到 node marks 属性中，通过 rich-text onTap 事件跳转。
