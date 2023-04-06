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
    "pages/index/index2"
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

# 注意事项
自定义 tabBar 默认 `z-index：10000`，若不满足项目实际场景可通过类名 `a-customize-tab-bar` 进行覆盖。
```css
/* app.acss */
.a-customize-tab-bar{
  z-index：999;
}
```
