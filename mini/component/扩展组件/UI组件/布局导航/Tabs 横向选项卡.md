
# 简介
当应用需要展示二级以上内容时，屏幕顶部会展示一个标签栏，并提供在应用的不同部分之间快速切换的功能。标签栏在所有屏幕方向上保持相同的高度。

选项：根据业务场景需要可以设定 2 个以上选项，当选项超过屏幕宽度后可以横滑选项行查看所有内容。

新内容标记：选项卡上能显示未读或者新内容标记。

场景描述：当选项卡内容提供给用户自定义配置时提供编辑/新建入口，用户可以由此进入编辑页面进行修改。

## 使用限制

- 通过触发 onChange 事件，设置 setData 对应的数据，从而切换页面上的 tabs 数据。
- 可使用 [my.request](https://opendocs.alipay.com/mini/api/owycmh)  传数据给后端。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*AptiT47jyXEAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=We6nKeYvCpiZLki_J91kbAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-tabs?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "Tabs 横向选项卡",
 "usingComponents": {
   "tabs": "mini-ali-ui/es/tabs/index",
   "tab-content": "mini-ali-ui/es/tabs/tab-content/index"
 }
}
```

### .axml 示例代码
```html
<view style="padding:24px;">
<tabs tabs="{{tabs}}"
  tabsName="activeTab"
  onTabClick="handleTabClick"
  onChange="handleTabChange"
  onPlusClick="handlePlusClick"
  activeTab="{{activeTab}}"
  showPlus="{{hasPlus}}"
  swipeable="{{false}}"
  capsule="{{typeCapsule}}"
  hasSubTitle="{{typeHasSubTitle}}"
  tabBarUnderlineWidth="20px"
  tabContentHeight="{{activeTab === 0 ? '130px' : activeTab === 2 ? '200px' : '50vh'}}"
  stickyBar="{{true}}">
  <block a:for="{{tabs}}">
    <tab-content key="{{index}}"
      tabId="{{index}}"
      activeTab="{{activeTab}}"
      a:if="{{index === 0}}">
      <view class="tab-content"
        style="height: 130px;">高度为 130px {{item.title}}</view>
    </tab-content>
    <tab-content key="{{index}}"
      tabId="{{index}}"
      activeTab="{{activeTab}}"
      a:elif="{{index === 2}}">
      <view class="tab-content"
        style="height: 200px;">改变 tab-content 高度为 200px {{item.title}}</view>
    </tab-content>
    <tab-content key="{{index}}"
      tabId="{{index}}"
      activeTab="{{activeTab}}"
      a:else>
      <view class="tab-content">content of {{item.title}}</view>
    </tab-content>
  </block>
 </tabs>
</view>
<view class="demo-title">elevator 模式: </view>
<navigator url="./elevator/elevator"
  open-type="redirect"
  style="padding: 24rpx 40rpx;">点击进入 elevator 电梯组件模式</navigator>
<view class="demo-title">tab 类型: </view>
<radio-group class="radio-group"
  onChange="typeChange"
  name="type">
  <label class="radio"
    a:for="{{type}}"
    key="label-{{index}}">
    <radio value="{{item.name}}"
      checked="{{item.checked}}" />
    <text class="radio-text">{{item.value}}</text>
  </label>
</radio-group>
<view class="demo-title">是否有 ➕icon: </view>
<radio-group class="radio-group"
  onChange="plusChange"
  name="plus">
  <label class="radio"
    a:for="{{plus}}"
    key="label-{{index}}">
    <radio value="{{item.name}}"
      checked="{{item.checked}}" />
    <text class="radio-text">{{item.value}}</text>
  </label>
</radio-group>
<view class="demo-title">tabs选项数量: </view>
<radio-group class="radio-group"
  onChange="tabsNumberChange"
  name="tabsNumber">
  <label class="radio"
    a:for="{{tabsNumber}}"
    key="label-{{index}}">
    <radio value="{{item.name}}"
      checked="{{item.checked}}" />
    <text class="radio-text">{{item.value}}</text>
  </label>
</radio-group>
```

### .js 示例代码
```javascript
Page({
  data: {
    tabs: [
      {
        title: '选项',
        subTitle: '描述文案',
        number: '6',
        showBadge: true,
        badge: {
          arrow: true,
          stroke: true,
        },
      },
      {
        title: '选项二',
        subTitle: '描述文案描述',
        number: '66',
        showBadge: true,
        badge: {
          arrow: false,
          stroke: true,
        },
      },
      {
        title: '3 Tab',
        subTitle: '描述',
        number: '99+',
        showBadge: true,
        badge: {
          arrow: true,
        },
      },
      {
        title: '4 Tab',
        subTitle: '描述',
        showBadge: true,
        number: 0,
      },
      {
        title: '5 Tab',
        subTitle: '描述描述',
        number: '99+',
        showBadge: false,
      },
      {
        title: '3 Tab',
        subTitle: '描述',
        showBadge: false,
      },
      {
        title: '4 Tab',
        subTitle: '描述',
      },
      {
        title: '15 Tab',
        subTitle: '描述',
      },
    ],
    activeTab: 0,
    type: [
      { name: 'normal', value: '普通', checked: true },
      { name: 'capsule', value: '胶囊' },
      { name: 'hasSubTitle', value: '带描述' },
    ],
    typeCapsule: false,
    typeHasSubTitle: false,
    plus: [
      { name: 'has', value: '是', checked: true },
      { name: 'hasnt', value: '否' },
    ],
    hasPlus: true,
    contentHeight: [
      { name: 'has', value: '是' },
      { name: 'hasnt', value: '否', checked: true },
    ],
    tabsNumber: [
      { name: '1', value: '一条' },
      { name: '2', value: '两条' },
      { name: '3', value: '三条' },
      { name: '-1', value: '很多', checked: true },
    ],
  },
  tabsNumberChange(e) {
    if (e.detail.value === '1') {
      this.setData({
        tabs: [
          {
            title: '选项',
            subTitle: '描述文案',
            number: '6',
          },
        ],
      });
    } else if (e.detail.value === '2') {
      this.setData({
        tabs: [
          {
            title: '选项',
            subTitle: '描述文案',
            number: '6',
            showBadge: true,
            badge: {
              arrow: true,
              stroke: true,
            },
          },
          {
            title: '选项二',
            subTitle: '描述文案描述',
            number: '66',
            showBadge: true,
          },
        ],
      });
    } else if (e.detail.value === '3') {
      this.setData({
        tabs: [
          {
            title: '选项',
            subTitle: '描述文案',
            number: '6',
            showBadge: true,
            badge: {
              arrow: true,
              stroke: true,
            },
          },
          {
            title: '选项二',
            subTitle: '描述文案描述',
            number: '66',
            showBadge: true,
          },
          {
            title: 'Tab',
            subTitle: '描述',
            number: '99+',
            showBadge: true,
            badge: {
              arrow: true,
              stroke: false,
            },
          },
        ],
      });
    } else {
      this.setData({
        tabs: [
          {
            title: '选项',
            subTitle: '描述文案',
            number: '6',
            showBadge: true,
            badge: {
              arrow: true,
              stroke: true,
            },
          },
          {
            title: '选项二',
            subTitle: '描述文案描述',
            number: '66',
            showBadge: true,
            badge: {
              arrow: false,
              stroke: true,
            },
          },
          {
            title: '3 Tab',
            subTitle: '描述',
            number: '99+',
            showBadge: true,
            badge: {
              arrow: true,
            },
          },
          {
            title: '4 Tab',
            subTitle: '描述',
            showBadge: true,
            number: 0,
          },
          {
            title: '5 Tab',
            subTitle: '描述描述',
            number: '99+',
            showBadge: false,
          },
          {
            title: '3 Tab',
            subTitle: '描述',
            showBadge: false,
          },
          {
            title: '4 Tab',
            subTitle: '描述',
          },
          {
            title: '15 Tab',
            subTitle: '描述',
          },
        ],
      });
    }
  },
  typeChange(e) {
    if (e.detail.value === 'hasSubTitle') {
      this.setData({
        typeCapsule: true,
        typeHasSubTitle: true,
      });
    } else if (e.detail.value === 'capsule') {
      this.setData({
        typeCapsule: true,
        typeHasSubTitle: false,
      });
    } else {
      this.setData({
        typeCapsule: false,
        typeHasSubTitle: false,
      });
    }
  },
  plusChange(e) {
    if (e.detail.value === 'hasnt') {
      this.setData({
        hasPlus: false,
      });
    } else {
      this.setData({
        hasPlus: true,
      });
    }
  },
  handleTabClick({ index, tabsName }) {
    this.setData({
      [tabsName]: index,
    });
  },
  handleTabChange({ index, tabsName }) {
    this.setData({
      [tabsName]: index,
    });
  },
  handlePlusClick() {
    my.alert({
      content: 'plus clicked',
    });
  },
});
```

### .acss 示例代码
```css
.tab-content {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 40rpx;
  box-sizing: border-box;
  /* 如果 swipeable="{{true}}"，需要增加 height */
  /* height: 350px; */
  /* 为了体现 stickyBar 的作用而增加的 tab-content 的高度 */
  height: 50vh;
}
.radio-group {
  padding: 30rpx 40rpx 0;
}
.radio {
  margin-right: 10px;
}
.demo-title {
  margin: 30rpx 40rpx 0;
  padding-bottom: 10px;
  font-weight: bold;
  border-bottom: 1px solid #ccc;
}
```

## 属性说明
tabs 横向选项卡主要是由 `<tabs>` 和 `<tab-content>` 两个标签组成，包含的类型较多，可通过 `<tabs>` 的属性进行配置，

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | - | 自定义 class。 |
| activeCls | String | - | 自定义激活 tabbar 的 class（设置字体样式和宽度）。 |
| tabs | Array | true | tab 数据，其中包括选项标题 title、副标题（描述）文案 subTitle、胶囊形式 tab 中的数字 number，如需要以 badge 方式展示数字，添加 showBadge 并设置为 true 即可。<br />**版本要求：** mini-ali-ui [1.0.9](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上支持 showBadge |
| activeTab | Number | true | 当前激活的 Tab 索引。<br />**默认值：** 0 |
| tabBarCls | String | - | tabbar的自定义样式 class。 |
| tabBarUnderlineColor | String | - | 选中选项卡下划线颜色。<br />**默认值：** #1677FF |
| tabBarActiveTextColor | String | - | 选中选项卡字体颜色。<br />**默认值：** #1677FF |
| capsuleTabBarActiveTextColor | String | - | 胶囊选中选项卡字体颜色。<br />**默认值：** #ffffff |
| capsuleTabBarBackgroundColor | String | - | 胶囊未选中的背景色。<br />**默认值：** #e5e5e5<br />**版本要求：mini-ali-ui** [1.0.12](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| tabBarInactiveTextColor | String | - | 未选中选项卡字体颜色。<br />**默认值：** #333333 |
| tabBarSubTextColor | String | - | 未选中描述字体颜色。<br />**默认值：** #999999 |
| tabBarActiveSubTextColor | String | - | 选中描述字体颜色。<br />**默认值：** #ffffff |
| tabBarBackgroundColor | String | - | 选项卡背景颜色。<br />**默认值：** #ffffff |
| showPlus | Boolean | - | 是否显示 + icon。<br />**默认值：** false |
| swipeable | Boolean | - | tabs 内容区是否可拖动。<br />**默认值：** true |
| animation | Boolean | - | 选项卡切换时滑动动画。<br />**默认值：** true |
| duration | Number | - | tabs 内容区切换动画时长。<br />**默认值：** 500 |
| capsule | Boolean | - | 是否为胶囊 tab。<br />**默认值：** false |
| hasSubTitle | Boolean | - | 是否有副标题（描述）内容。<br />**默认值：** false |
| elevator | Boolean | - | 是否电梯组件。<br />**默认值：** false |
| elevatorTop | String | - | 电梯组件中 tab 置顶时的位置控制。<br />**默认值：** 0 px<br />**版本要求：** mini-ali-ui [1.0.8](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| elevatorContentTop | Number | - | 电梯组件中 tab-content 距离顶部的位置。<br />**默认值：** 0<br />**版本要求：** mini-ali-ui [1.0.10](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| onPlusClick | EventHandle | - | + icon 被点击时的回调。<br />**默认值：** () => {} |
| onTabClick | EventHandle | - | tab 被点击的回调。<br />**默认值：** (index: Number，tabsName：String) => void |
| onChange | EventHandle | - | tab 变化时触发。<br />**默认值：** (index: Number，tabsName：String) => void |
| tabsName | String | true | tab 选项卡的名字，与 activeTab 的 key 值相同。 |
| tabBarUnderlineWidth | String | - | 设置 tab 选项卡选中态的下划线宽度。<br />**默认值：** 100%<br />**版本要求：** mini-ali-ui [1.0.10](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| tabBarUnderlineHeight | String | - | 设置 tab 选项卡选中态的下划线高度。<br />**默认值：** 2px<br />版本要求：mini-ali-ui [1.0.10](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| onTabFirstShow | EventHandle | - | tab 选项卡首次出现时的回调。<br />**默认值：** (index: Number, tabsName: String) => {}<br />**版本要求：** mini-ali-ui [1.0.12](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| tabContentHeight | String | - | 当 swipeable 为 true 时，可通过该属性值重设高度强制让 swiper 组件支持“自适应”高度的行为。<br />**版本要求：** mini-ali-ui [1.0.12](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| plusIcon | String | - | icon 类型可参考 [am-icon 类型](https://opendocs.alipay.com/mini/component-ext/am-icon#type%20%E6%9C%89%E6%95%88%E5%80%BC)。<br />**默认值：** add<br />**版本要求：** mini-ali-ui [1.1.4](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| plusIconSize | Number | - | 改变 icon 大小。<br />**默认值：** 16<br />**版本要求：** mini-ali-ui [1.1.4](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| plusIconColor | String | - | 改变 icon 颜色。<br />**版本要求：** mini-ali-ui [1.1.4](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| plusImg | String | - | 使用图片替换 icon。<br />**版本要求：** mini-ali-ui [1.1.4](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| plusImgWidth | String | - | 设置替换 icon 后的图片宽度。<br />**版本要求：** mini-ali-ui [1.1.4](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| plusImgHeight | String | - | 设置替换 icon 后的图片高度。<br />**版本要求：** mini-ali-ui [1.1.4](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| stickyBar | Boolean | false | tabBar 是否在页面滚动的时候定位在顶部的某个位置，可结合 elevatorTop 设置距离顶部的位置。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.1.5](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |


###  tab-content
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| index | String | 列表项的唯一索引。 |
| tabId | Number | tab 内容序列索引。<br />**默认值：** {{index}} |
| activeTab | Number | 选项卡当前激活序列索引。<br />**默认值：** {{activeTab}} |
| elevator | Boolean | 电梯组件时需要指定。<br />**默认值：** false |


## Bug & Tip

- `capsule` 为 true 时，tab 选项卡显示为胶囊模式。
- `hasSubTitle` 为 true 时，tabs 选项卡会显示带有描述的模式，但如果 tabs 数据中的 `subTitle` 为空，将不会显示描述文案。
- 当 tabs 选项卡为胶囊模式时，会根据 tabs 数据中的 `number` 值显示数字。
- 如 `elevator` 为 `true`，则为电梯组件，`<tab-content>` 将竖排展示，自动计算每个 `<tab-content>` 的坐标后，根据索引值定位指向；
   - 在 `elevator` 模式中，`this.data.floorNumber` 将会根据所有 **tab-content** 的高度计算所得，无需修改；
   - 电梯组件需要考虑页面滚动时判断每个 **tab-content** 的位置，因此需要在页面级别中加入 `onPageScroll({ scrollTop }) {}`，具体可参考代码示例中的代码；
- `tabsName` 是为了能更好获取到当前 tab 选项卡的名称进行识别，值需要与 `activeTab` 的 key 值相同，如：`activeTab="{{activeTab2}}"`，那么 `tabsName="activeTab2"`。
- tabs 中的 `showBadge` 为 true 时，`number` 中的值会以 `badge` 形式展示，并且不受 tab 类型影响，否则 `number` 中的值仅在胶囊 tab 中有效。
   - 可同时添加 `badge: { arrow: true, stroke: true, }` 控制 badge 的样式。
   - `arrow` 可展示有箭头的 badge，箭头仅有左方向。
   - `stroke` 可展示有描边的 badge。
- 当 `elevatorTop` 的值为 px 单位时，`elevatorContentTop` 距离顶部的高度则是 `elevatorTop` + tab 选项卡的高度。
- 当 `plusImg` 的值为空时才可以使用 `plusIcon`、 `plusIconSize` 以及 `plusIconColor` 这三个值。
- 当 `plusImg` 的值为空时， `plusImgWidth` 和 `plusImgHeight` 设置将无效。
- 如果 `plusIcon` 为空， `plusIconSize` 和 `plusIconColor` 修改的是默认的 icon 大小以及颜色。

### tab-content 高度自适应说明
tabs 组件内容区域高度是否能够自适应，需要注意 swipeable 的值：

- `swipeable='{{true}}'`：内容区域可滑动，且相对应 tab 标签卡；但内容区域高度为固定值，需要在 acss 文件中设定 height 值，否则高度会异常；如需要自适应高度的话，那么请使用 `tabContentHeight` 重设高度，实现方法：点击不同 tab 标签卡，获取当前 `tab-content` 的高度，赋值给 `tabContentHeight` 即可。
- `swipeable='{{false}}'`：内容区域不可滑动，此时高度表现形式有两种，且可以不需要在 acss 文件设定 height 值：
   - `<tab-content>` 中**无** `tabId` 和 `activeTab` 两个属性，此时的高度将以所有内容区域中最高的为基准展示。
   - `<tab-content>` 中**包含** `tabId` 和 `activeTab` 两个属性时 `tabId="{{index}}" activeTab="{{activeTab}}"`，内容区域所展示的高度将会随着不同模块的高度而改变。 
