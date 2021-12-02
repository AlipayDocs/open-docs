
# 简介
小程序开发者工具引入了设计模式，提供了可视化设计面板，让开发者可以通过拖拽的方式快速进行界面布局，同时支持代码和设计布局进行双向实时同步，使得小程序开发更加迅捷、简单和灵活。称之为可视化辅助编程，可视化辅助编程的目标不是取代编码本身，而是减少非必要的和重复的手工编码工作。可视化设计面板支持支付宝小程序所有的基础组件、扩展组件和自定义组件，供开发者灵活选择与使用。
![|723x503](https://gw.alipayobjects.com/zos/skylark-tools/public/files/7c9b1d2c4a9dcf3996b2479b6c9829c6.png?x-oss-process=image/resize,w_1500#align=left&display=inline&height=519&margin=%5Bobject%20Object%5D&originHeight=1044&originWidth=1500&status=done&style=none&width=746)

## 使用限制

- 支持小程序开发者工具 1.0 及以上版本。
- 支持支付宝和淘宝开发环境。

# 使用流程

## 进入设计模式
点击小程序开发者工具右上方按钮，从编码模式（IDE 的默认模式）进入设计模式。

**说明：** 在设计模式中，模拟器默认关闭，开发者可以随时点击模拟器顶部按钮唤起模拟器，模拟器将以独立窗口弹出。

![|723x469](https://gw.alipayobjects.com/zos/skylark-tools/public/files/14951379d92241b35d24904a1c327ef8.png?x-oss-process=image/resize,w_1500#align=left&display=inline&height=484&margin=%5Bobject%20Object%5D&originHeight=974&originWidth=1500&status=done&style=none&width=746)

开发者可以随时切换回编码模式。

![|723x466](https://gw.alipayobjects.com/zos/skylark-tools/public/files/dfd584cff82500c1698a33f6a6a62611.png?x-oss-process=image/resize,w_1500#align=left&display=inline&height=481&margin=%5Bobject%20Object%5D&originHeight=967&originWidth=1500&status=done&style=none&width=746)

## 选择小程序页面
开发者如果打开小程序页面里面 axml、css、js、json 里面的任何一个文件，画布会自动定位到该页面。

**注意：** 如果没有选择页面，默认定位到小程序第一个页面；画布也支持自定义组件页面的可视化设计。

![|723x452](https://gw.alipayobjects.com/zos/skylark-tools/public/files/3d36014a29897449259e616eaaed6616.png?x-oss-process=image/resize,w_1500#align=left&display=inline&height=466&margin=%5Bobject%20Object%5D&originHeight=938&originWidth=1500&status=done&style=none&width=746)

## 添加和编辑组件
开发者可以直接从组件面板拖拽到画布或者组件树，然后点击组件，在右边的设置 TAB 里面设置组件的属性、样式、事件和查看组件帮助文档。

**注意：** 首次添加扩展组件时，因为会自动从网络下载并安装 `mini-ali-ui` NPM 包，所以需要确保网络处于连接状态，如果安装失败，需要到 NPM 管理界面手工安装 `mini-ali-ui` NPM 包。

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fdbf5f8d08c925560243e53dd65550a5.gif#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=960&status=done&style=none&width=746)

## 添加自定义组件
开发者可以直接拖拽自定义组件到画布中，详情请参见 [自定义组件](https://opendocs.alipay.com/mini/framework/custom-component-overview)。

**注意：** 不要点击打开自定义组件里面的文件，否则画布自动切换到自定义组件页面。

![|723x452](https://gw.alipayobjects.com/zos/skylark-tools/public/files/441d46e45731a162851ea996800dbd21.png?x-oss-process=image/resize,w_1500#align=left&display=inline&height=466&margin=%5Bobject%20Object%5D&originHeight=938&originWidth=1500&status=done&style=none&width=746)

## 唤起模拟器查看运行时效果
画布只能在设计时渲染页面的静态结构和行为，并不能完全展示页面的动态行为，需要运行模拟器查看运行时效果。开发者可以点击运行模拟器按钮唤起模拟器。

**注意：** 需要保存文件以在模拟器中生效。

![|723x469](https://gw.alipayobjects.com/zos/skylark-tools/public/files/931188a6abb5b53095ab9a8242866685.png?x-oss-process=image/resize,w_1500#align=left&display=inline&height=484&margin=%5Bobject%20Object%5D&originHeight=974&originWidth=1500&status=done&style=none&width=746)

## 相关信息

- [组件](https://opendocs.alipay.com/mini/component) 
- [自定义组件](https://opendocs.alipay.com/mini/framework/custom-component-overview)

## 问题反馈
如果在使用过程中有任何问题和反馈，请扫码进入钉钉群获得快捷支持。

![|324x389](https://mdn.alipayobjects.com/afts/img/A*YDMTTZ8r1x4AAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=xDK-twjfAUdbE748mZcGAQAAAABkMK8AAAAA#align=left&display=inline&height=389&margin=%5Bobject%20Object%5D&originHeight=389&originWidth=324&status=done&style=none&width=324)
