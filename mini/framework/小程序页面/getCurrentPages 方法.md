`getCurrentPages()` 获取当前页面栈的实例，将页面栈的数据以数组的形式返回。第一个元素为首页，最后一个元素为当前页面。

小程序以栈的形式维护当前的所有页面。路由切换与页面栈的关系如下：

| **路由方式** | **页面栈表现** |
| --- | --- |
| 初始化 | 新页面入栈 |
| 打开新页面 | 新页面入栈 |
| 页面重定向 | 当前页面出栈，新页面入栈 |
| 页面返回 | 当前页面出栈 |
| Tab切换 | 页面全部出栈，只留下新的 Tab 页面 |

**注意：** 不要尝试修改页面栈，会导致路由以及页面状态错误。

## 入参
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| getAllPages | Boolean | 获取到当前页面栈的所有实例。<br /> 如果是在宿主内调用，获取到的插件页面实例只是一个代理，只能获取到基本的 `route` 信息，无法调用页面内的方法，反之亦然。<br /> **默认值**：false。<br />**版本要求**：基础库 [2.7.7](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上。 |


## 示例代码
可以用于检测当前页面栈是否具有 5 层页面深度：
```javascript
if (getCurrentPages().length === 5) {
  my.redirectTo({
    url: '/pages/logs/logs'
  });
} else {
  my.navigateTo({
    url: '/pages/index/index'
  });
}
```
假设当前页面栈：宿主小程序 A，插件 B，宿主小程序 C。默认地，宿主小程序和插件之间无法访问到各自的页面：
```json
// 宿主小程序内调用
// 返回结果: [宿主A，null，宿主C]
getCurrentPages()[1] === null; // true

// 插件内调用
// 返回结果: [null，插件B，null]
getCurrentPages()[0] === null; // true
```
通过指定 `getAllPages`，可以获得代理实例，取得 `route` 信息：
```javascript
// 宿主小程序内调用
// 返回结果: [宿主A，插件B_Proxy，宿主C]
getCurrentPages({
 getAllPages: true
})[1].route; // 插件B页面的路径

// 插件内调用
// 返回结果: [宿主A_Proxy，插件B，宿主C_Proxy]
getCurrentPages({
 getAllPages: true
})[0].route; // 宿主小程序A页面的路径
```

## 常见问题

### Q：getCurrentPages 方法怎么获取页面路径？
A：`getCurrentPages()[N].route`，可以获取到页面路径（N 为页面数组栈中页面对象所在序号，最大值为当前页）。

### Q：getCurrentPages 方法可以获取到参数吗？
A：不可以，只能获取页面栈，无法获取参数。

## 相关文档

- [页面常见问题](https://opendocs.alipay.com/mini/framework/page-faq)
- [页面运行机制](https://opendocs.alipay.com/mini/framework/page-detail)

