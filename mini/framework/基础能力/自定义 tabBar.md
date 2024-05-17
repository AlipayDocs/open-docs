# 简介
[tabBar](https://opendocs.alipay.com/mini/00prvl) 作为支付宝小程序基础能力，提供底部操作栏进行切换页面。自定义 tabBar 作为补充能力，可以让开发者更加灵活地设置 tabBar，以满足更多个性化的场景。<br />在自定义 tabBar 模式下：

- 开发者需要提供一个自定义组件来进行 tabBar 的渲染及交互。
- 与 tabBar 样式相关的接口将失效。如 [my.hideTabBar](https://opendocs.alipay.com/mini/api/at18z8) 等。
- 每个页面的 tabBar 组件实例是不同的，可通过 [getTabBar](https://opendocs.alipay.com/mini/framework/page-detail#Page.getTabBar) 接口获取 tabBar 组件实例。

## 版本要求

- 基础库 2.7.20 及以上版本。
- 支付宝客户端 10.2.63 及以上版本。
- [小程序开发者工具](https://opendocs.alipay.com/mini/ide/overview) 3.1.2 及以上版本。

若版本较低，则显示原始 tabBar，为保证兼容性，tabBar 的相关配置**建议完整声明**。

# 使用流程

## 1. 配置信息
在现有 tabBar 配置基础上新增`customize`字段。

### app.json 示例
```json
{
	"pages": [
    "pages/index/index",
    "pages/index2/index"
  ],
  "tabBar": {
    "customize": true,
    "items": [
      {
        "pagePath": "pages/index/index",
        "name": "Tab 1"
      },
      {
        "pagePath": "pages/index2/index",
        "name": "Tab 2"
      }
    ]
  }
}
```

## 2. 添加 tabBar 文件
约定在代码根目录下添加 tabBar 入口文件。
```powershell
├── customize-tab-bar				# 自定义 tabBar 文件
│   ├── index.acss
│   ├── index.axml
│   ├── index.js
│   └── index.json
├── components
│		└── ...
├── pages
│		└── ...
├── app.acss
├── app.js
├── app.json
├── mini.project.json
└── ...
```

## 3. 编写 tabBar 代码
编码规范可查看 [自定义组件](https://opendocs.alipay.com/mini/framework/custom-component-overview)。该自定义组件将完全接管 tabBar 的渲染及交互，同时，新增 [getTabBar](https://opendocs.alipay.com/mini/framework/page-detail#Page.getTabBar) 接口可获取自定义 tabBar 组件实例。

### 示例代码

#### customize-tab-bar/index.axml
```html
<view class="tab-bar">
  <view a:for="{{list}}" onTap="tap" data-value={{item}} data-index={{index}} class="item">
    <view style="color: {{selected == index ? selectedColor : textColor}}">{{item.name}}</view>
  </view>
</view>
```

#### customize-tab-bar/index.js
```javascript
Component({
  data: {
    selected: 0,
    textColor: "#7A7E83",
    selectedColor: "#2f54eb",
    list: [
      {
        pagePath: "/pages/index/index",
        name: "customize1",
      },
      {
        pagePath: "/pages/index2/index",
        name: "customize2",
      },
    ],
  },
  methods: {
    tap(e) {
      const data = e.target.dataset;
      my.switchTab({
        url: data.value.pagePath,
      });
    },
  },
})
```

#### pages/index/index.js
```javascript
Page({
  onShow() {
    if (typeof this.getTabBar === 'function' && this.getTabBar()) {
      this.getTabBar().setData({
        selected: 0,
      });
    }
  },
})
```


# 自定义 tabBar 原生渲染模式
自定义 tabBar 为开发者带来了开发更具表现力的 tabBar 能力，但对比原生 tabBar，存在一些体验问题。</br>

1. 自定义 tabBar 由于渲染在页面视图内，所以在点击 tabBar 切换页面时，tabBar 存在 **闪烁** 问题。</br>
2. 同理，当启用页面下拉刷新时，tabBar 将在整个页面下拉过程中跟随移动，导致部分不可见。</br>
效果对比：</br>

| **操作** | **普通自定义 tabBar** | **Native 自定义 tabBar**  |
| -------- | -------- | ---------------- |
| 切换页面  | <img src="https://mdn.alipayobjects.com/portal_mdssth/afts/img/A*68A6Qo5lceYAAAAAAAAAAAAAAQAAAQ/original" width="250px" >       | <img src="https://mdn.alipayobjects.com/portal_mdssth/afts/img/A*8QRmSqiG4IIAAAAAAAAAAAAAAQAAAQ/original" width="250px">      |
| 下拉刷新 | <img src="https://mdn.alipayobjects.com/portal_mdssth/afts/img/A*_fa0SaP-5UAAAAAAAAAAAAAAAQAAAQ/original" width="250px" >      | <img src="https://mdn.alipayobjects.com/portal_mdssth/afts/img/A*MNTfQp-WwPYAAAAAAAAAAAAAAQAAAQ/original" width="250px">  |
</br>

造成上述效果差异的原因在于普通自定义 tabBar 和 Native 自定义 tabBar 在渲染模型上存在差异。Native 自定义 tabBar 独立于页面且覆盖在页面之上，普通自定义 tabBar 跟随页面一起渲染。</br>

![900x400](https://mdn.alipayobjects.com/portal_mdssth/afts/img/A*I1GTT4e6EdgAAAAAAAAAAAAAAQAAAQ/original)

## 如何启用
这是一种特殊的自定义 tabBar 运行模式，开发者可通过修改 `app.json` 内的 `tabBar` 字段配置启用。
```json
{
  ...
  "tabBar": {
    "customize": true,
    "overlay": true, /* 启用 Native 模式 */
  }
}
```
**注意**：如未配置 `customize:true`，则 `overlay:true` 配置无效。
配置完成后，框架将在小程序运行环境允许的情况下自动将自定义 tabBar 渲染为 Native 模式。

## 调试预览

虽然 Native 自定义 tabBar 开发范式与普通自定义 tabBar 完全一致，但由于使用了 Native 渲染引擎，所以在诸如样式支持度及基础组件支持度上与普通自定义 tabBar 存在差异，所以在配置完成后，开发者需要手动确认其表现是否符合预期。</br>
由于目前不支持在 IDE 模拟器内预览调试 Native 自定义 tabBar，开发者需要通过 **真机预览** 或 **真机调试** 进行预览和测试。</br>
请使用以下环境进行：</br>
- 基础库 2.9.10 及以上。</br>
- 支付宝客户端 10.5.70 及以上。</br>


## 运行时检测

当配置 `overlay:true` 后，原本「自定义 TabBar 」的 [接口](https://opendocs.alipay.com/mini/03jry7) `this.getTabBar()` 返回的自定义组件实例上，会新增一个属性 `overlay: boolean`。
```javascript
Page({
  onShow() {
    const customizeTabBar = typeof this.getTabBar === 'function' && this.getTabBar();
    if (customizeTabBar && customizeTabBar.overlay) {
      // Native 自定义 tabBar
    }
  },
})
```


## 兼容性处理
1. 可根据上述 `this.getTabBar().overlay` 判断目前所处于的渲染模式，用于处理新老模式之间的差异。
2. 在不满足运行条件时，均会自动降级至普通版本的自定义 tabBar。


### 弹层覆盖
由于[上述](https://opendocs.alipay.com/mini/03jry7?pathHash=148d378a#%E8%87%AA%E5%AE%9A%E4%B9%89%20tabBar%20%E5%8E%9F%E7%94%9F%E6%B8%B2%E6%9F%93%E6%A8%A1%E5%BC%8F)渲染模型之间的差异，当开发者将自定义 tabBar 切换到 Native 渲染后，需要重点关注业务中的弹层与自定义 tabBar 的相互覆盖关系。</br>
开发者通过 `axml` 代码显示的弹层均将被 Native 自定义 tabBar 覆盖且通过修改自定义 tabBar 的 `z-index` 属性将无法做到调整覆盖层级。

| **普通自定义 tabBar** | **Native 自定义 tabBar**  |
| -------- | ---------------- |
| <img src="https://mdn.alipayobjects.com/portal_mdssth/afts/img/A*UvNYSoz-_HgAAAAAAAAAAAAAAQAAAQ/original" width="333px" height="720px" >       |<img src="https://mdn.alipayobjects.com/portal_mdssth/afts/img/A*OT4bTJ_JYW8AAAAAAAAAAAAAAQAAAQ/original" width="333px" height="720px" > |

**说明**：目前阶段，需要开发者在显示弹层组件时，手动对 tabBar 内元素进行隐藏（如 `a:if="{{visible}}"`）。</br>

## 常见问题

### Q: 使用 Native 自定义 tabBar 是否需要开启当前页面的 Native 渲染？</br>
A：不需要。在不开启页面的 Native 渲染模式下，也可单独启用 Native 自定义 tabBar。
### Q：遇到不支持的样式如何处理？</br>
A: 样式支持度与 Native 渲染一致，样式支持度文档将在近期对外开放 。 

# 注意事项
自定义 tabBar 默认 `z-index:10000`，若不满足项目实际场景可通过类名 `a-customize-tab-bar` 进行覆盖。**Native 自定义 tabBar 不支持该特性**。
```css
/* app.acss */
.a-customize-tab-bar{
  z-index:999;
}
```

