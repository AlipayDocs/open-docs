`getCurrentPages()` 获取当前页面栈的实例，并将页面栈的信息以数组方式返回。数组的第一个元素代表首页，最后一个元素代表当前页面。

小程序通过页面栈的形式来维护当前所有页面。路由切换时，页面栈会有以下变化：

| 路由方式 | 页面栈表现                       |
| -------- | -------------------------------- |
| 初始化   | 新页面入栈。                     |
| 打开新页面 | 新页面入栈。                     |
| 页面重定向 | 当前页面出栈，新页面入栈。         |
| 页面返回 | 当前页面出栈。                     |
| Tab 切换 | 所有页面出栈，只留下新的 Tab 页面。 |

**注意：** 不要试图修改页面栈，否则可能导致路由和页面状态出现问题。

# 入参

| 属性         | 类型    | 描述                                                         |
| ------------ | ------- | ------------------------------------------------------------ |
| getAllPages  | Boolean | 是否获取当前页面栈的所有实例。<br />如果是在宿主内调用，获取插件页面实例时只能得到 `route` 等基础信息，不可调用页面内方法，插件内调用亦是如此。<br />**默认值**：`false`。<br />**版本要求**：基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上版本可用。 |
# 示例代码

你可以使用下面的示例代码来检测当前页面栈是否具有 5 层页面深度：

```javascript
if (getCurrentPages().length === 5) {
  my.redirectTo({
    url: '/pages/logs/logs',
  });
} else {
  my.navigateTo({
    url: '/pages/index/index',
  });
}
```

假定当前页面栈的情况是：宿主小程序 A，插件 B，宿主小程序 C。默认情况下，宿主小程序和插件之间不能相互访问对方的页面：

```json
// 宿主小程序内调用
// 返回结果：[宿主 A，null，宿主 C]
getCurrentPages()[1] === null; // true

// 插件内调用
// 返回结果：[null，插件 B，null]
getCurrentPages()[0] === null; // true
```

通过指定 `getAllPages` 参数，你可以获取代理实例并获取 `route` 信息：

```javascript
// 宿主小程序内调用
// 返回结果：[宿主 A，插件 B_Proxy，宿主 C]
getCurrentPages({
  getAllPages: true,
})[1].route; // 插件 B 页面的路径

// 插件内调用
// 返回结果：[宿主 A_Proxy，插件 B，宿主 C_Proxy]
getCurrentPages({
  getAllPages: true,
})[0].route; // 宿主小程序 A 页面的路径
```
# 常见问题

## Q：`getCurrentPages` 方法如何获取页面路径？

A：通过 `getCurrentPages()[N].route` 可以获取到页面路径（`N` 为页面数组栈中页面对象所在序号，最大值为当前页）。

## Q：`getCurrentPages` 方法可以获取到参数吗？

A：不可以，它只能获取页面栈，无法获取参数。

# 相关文档

- [页面常见问题](https://opendocs.alipay.com/mini/framework/page-faq)
- [页面运行机制](https://opendocs.alipay.com/mini/framework/page-detail)
