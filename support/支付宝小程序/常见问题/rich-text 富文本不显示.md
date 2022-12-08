## 场景分析
rich-text 富文本不显示，传输的 HTML 数据正常但是不渲染，显示不了图片等。 

## 解决方案

1. 根据文档排查 HTML 数据是否存在不支持的标签、属性、样式。

**注意**：

   - [rich-text 富文本](https://opendocs.alipay.com/mini/component/rich-text) 组件支持 a 标签，不支持 href 超链接。
   - 富文本中的 JS 不支持事件执行。
   - nodes 属性只支持使用 Array 类型。如果需要支持 HTML String，则需要自己将 HTML String 转化为 nodes 数组，可使用 [mini-html-parser](https://github.com/ant-mini-program/mini-html-parser) 转换。
2. 检查每一对标签是否正常闭合。例如：有些编辑器 img 标签会出现没有闭合的情况 <img src="">，需要加上闭合符 <img src=""/>。
3. 使用 [mini-html-parser](https://github.com/ant-mini-program/mini-html-parser) 转换的 HTML String，可以添加一个 log 日志检查转换的 nodes 数组是否正常。
4. 检查基础库版本：要求基础库版本 1.11.0 或更高版本；若版本较低，建议做 [兼容](https://opendocs.alipay.com/mini/framework/compatibility) 处理。

 <br /> 
