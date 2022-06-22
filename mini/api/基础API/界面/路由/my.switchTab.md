# 简介
**my.switchTab** 跳转到指定标签页（[tabBar](https://opendocs.alipay.com/mini/framework/app-json#tabBar)）页面，并关闭其他所有非标签页页面。

通过页面跳转（[my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx)）或者页面重定向（[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky)）所到达的页面，即使是定义在标签页配置中的页面，也不会显示底部的标签栏。

## 使用限制
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/e88923c5934173d172f53342d823d838.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

### .js 示例代码
```javascript
my.switchTab({
  url: '/page/logs/index'
})
// 以下格式的 url 均支持(假如当前在 tab bar 页面 pages/index/index)：
// {url : '/page/logs/index'} 切换到 tab bar 页面 pages/logs/index 页面；
// {url : '../logs/index'} 切换到 tab bar 页面 pages/logs/index 页面；
// {url : 'index2'} 切换到 tab bar 页面 pages/index/index2, {url : 'index2'} 相对于当前路径，相当于 {url : './index2'}。
```

### [tabBar 配置](https://opendocs.alipay.com/mini/framework/app-json#tabBar)示例：
```app.json
{
  "pages": [
    "pages/index/index",
    "pages/index/index2",
    "pages/logs/index"
  ],
  "tabBar": {
    "items": [
      {
        "pagePath": "pages/index/index",
        "name": "首页"
      },
      {
        "pagePath": "pages/index/index2",
        "name": "测试"
      },
      {
        "pagePath": "pages/logs/index",
        "name": "日志"
      }
    ]
  }
}
```


## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 跳转的标签页的路径（需在 app.json 的 tabbar 字段定义的页面），支持相对路径和绝对路径。<br />**注意**：路径后不能带参数。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码

<table>
  <tr>
    <th><b>error</b></th>
    <th><b>errorMessage</b></th>
    <th><b>描述</b></th>
  </tr>
  <tr>
    <td rowspan="4">1</td>
    <td><code>${url} resolved to ${pagePath} is not found</code></td>
    <td>目标页面路径不存在。</td>
  </tr>
  <tr>
    <td><code>${url} is not found in plugin</code></td>
    <td>目标页面是插件页面，但该插件并没有声明该页面。</td>
  </tr>
  <tr>
    <td><code>${url} resolved to ${pagePath} is not tab,  which is not valid</code></td>
    <td>my.switchTab 只允许跳转到选项卡（tabbar）页面。</td>
  </tr>
  <tr>
    <td><code>plugin can not use switchTab</code></td>
    <td>不支持插件调用 my.switchTab。</td>
  </tr>
</table>
